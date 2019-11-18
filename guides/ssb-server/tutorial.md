# Introduction to Using ssb-server

This tutorial will help you familiarize with ssb-server, so you can build scripts and applications.

ssb-server is pretty unusual compared to datastores like MySQL or Redis, so let's get started with some basics.

## What is ssb-server?

ssb-server is a peer-to-peer log store.
Its data model is similar to that of [Apache Kafka](https://kafka.apache.org/), and it's part of a pattern that's now referred to as the [Kappa Architecture](http://kappa-architecture.com/).

What is Kappa Architecture?

 > Kappa Architecture is a software architecture pattern.
 Rather than using a relational DB like SQL or a key-value store like Cassandra, the canonical data store in a Kappa Architecture system is an append-only immutable log.
 From the log, data is streamed through a computational system and fed into auxiliary stores for serving.

So, imagine if Twitter supported JSON posts, and allowed more characters.
Now imagine your JSON-Twitter was also peer-to-peer.

In a nutshell, that's ssb-server.

## How do you write applications with it?

While feeds of JSON messages may seem pretty limited, they're actually able to support some pretty complex data-structures.

For instance, imagine we wanted to write a new file-sharing app.
To declare a new "package" of files, we might just publish a message like this:

```js
{
  type: 'create-file-package',
  package: 'My Files Package'
}
```

Then, we could add files with some more messages:

```js
{
  type: 'add-file-to-package',
  package: 'My Files Package',
  name: 'hello-world.txt',
  fileData: 'Hello, world!'
}
{
  type: 'add-file-to-package',
  package: 'My Files Package',
  name: 'my-picture.jpg',
  fileData: fs.readFileSync('./my-picture.jpg').toString('base64')
}
```

And then decide that, no, maybe that picture shouldnt be in the package:

```js
{
  type: 'remove-file-from-package',
  package: 'My Files Package',
  name: 'my-picture.jpg'
}
```

With the right processing code, we could easily scan these messages and produce a predictable output state, in the form of a data-structure:

```js
{
  package: 'My Files Package',
  files: { 'hello-world.txt': 'Hello, world!' }
}
```

And that's exactly how ssb-server applications work.
So, let's dig into the practical steps of making that happen.

## Setup the Server

The first step is to [install](./install.html) ssb-server.
You'll want the server running on the device that's running your application.

ssb-server is meant to be used on users' devices, in a P2P network.
It can be embedded ([Patchwork](https://ssbc.github.io/patchwork/) does this) but that's going to create conflicts after the user installs two ssb-server-embedding apps.
So, for now, it's best to tell your users to install and run ssb-server or Patchwork themselves, as dependencies to your app.

## Create the Client

The [ssb-client](https://github.com/ssbc/ssb-client) module can be used for making a connection to a running ssb-server process.

```js
var ssbClient = require('ssb-client')
ssbClient(function (err, sbot) {
  // ready
})
```

> ssb-server's CLI translates directly from the shell to RPC calls.
> That means any call you can make programmatically can be made from the shell as well.

## Publishing Messages

Publishing messages is very simple:

```js
sbot.publish({ type: type, ... }, cb)
```

Here's an example publish:

```js
sbot.publish({ type: 'post', text: 'hello, world' }, cb)
```

You are free to put anything you want in the message, with the following rules:

 - You must include a `type` attribute.
 - The output message, including headers, cannot exceed 8kb.

You can find [common message-schemas here](https://github.com/ssbc/ssb-msg-schemas).
For our toy file-publishing app, we'll make our own message schemas.

Let's create some convenience functions to do the publishing:

```js
function createPackage (sbot, package, cb) {
  sbot.publish({
    type: 'create-file-package',
    package: package
  }, cb)
}

function addFile (sbot, package, name, fileData, cb) {
  sbot.publish({
    type: 'add-file-to-package',
    package: package,
    name: name,
    fileData: fileData
  }, cb)
}

function removeFile (sbot, package, name, cb) {
  sbot.publish({
    type: 'remove-file-from-package',
    package: package,
    name: name
  }, cb)
}
```

Now it's a little easier to create the messages we published earlier:

```js
var pictureBase64 = fs.readFileSync('./my-picture.jpg').toString('base64')
createPackage(sbot, 'My Files Package')
addFile(sbot, 'My Files Package', 'hello-world.txt', 'Hello, world!')
addFile(sbot, 'My Files Package', 'my-picture.jpg', pictureBase64)
removeFile(sbot, 'My Files Package', 'my-picture.jpg')
```

## Attaching Files to Messages

Messages have an 8kb limit, including the headers that are automatically added, so it's not a good idea to try to cram base64-encoded files into them.
Instead, we should use ssb-server's blob-store to publish the files, which presently has a 5MB limit.

We'll add another function to do this:

```js
var fs = require('fs')
var pull = require('pull-stream') // will explain later
var toPull = require('stream-to-pull-stream')

function addFileFromDisk (sbot, package, name, filePath, cb) {
  // add the file to the local blobstore
  pull(
    toPull.source(fs.createReadStream(filePath)),
    sbot.blobs.add(function (err, fileId) {
      if (err)
        cb(err)
      else {
        // publish
        addFile(sbot, package, name, fileId, cb)
      }
    })
  )
}
```

And we can now use this function to publish our jpg:

```js
addFileFromDisk(sbot, 'My Files Package', 'my-picture.jpg', './my-picture.jpg')
```

The result is something more like this:

```js
{
  type: 'add-file-to-package',
  package: 'My Files Package',
  name: 'my-picture.jpg',
  fileData: '&RRELXJAxum631eq1ikj7+qngd3f6Dvz7eA1mZNHBPQ0=.sha256'
}
```

The value of `fileData` is now a [content-hash link](https://ssbc.github.io/docs/ssb/linking.html).
When other ssb-servers see it, they'll ask their peers for the blob that matches that sha256 hash.
That means the file will lag behind the message a little bit, but it'll get there eventually!

## Reading the Messages

Now that we've got the publishing handled, we need to read the messages in, and process them into our output state.

ssb-server uses [pull-streams](https://github.com/dominictarr/pull-stream).
In most cases, you'll use them like this:   

```js
pull(sbot.foo(), pull.drain(function (msg) {
  // process the message as it arrive
}, function (err) {
  // stream is over
}))
```

Or, like this

```js
pull(sbot.foo(), pull.collect(function (err, msgs) {
  // process all the messages after the stream ends
}))
```

We'll use them now with [createLogStream](http://ssbc.github.io/docs/api/ssb-server.html#createlogstream-source) to create a persistent live stream of messages.
As each message is added, either due to network-gossip, or by the local user, it will be emitted here:

```js
pull(sbot.createLogStream({ live: true }), pull.drain(processMsg))
```

## Processing the Messages

Let's create some in-memory data structures to hold onto the file-packages.

It's important to realize, that the order of messages is only preserved within a given user's feed.
If Bob publishes 3 messages in a row, then every user that syncs Bob's feed will get those 3 messages in the same order.
But, if Alice publishes a fourth message, other users will not know if her message came before Bob's 3 messages, after them, or somewhere in the middle.

This can be mitigated with [Content Hash Links](https://ssbc.github.io/docs/ssb/linking.html), which provides a guaranteed "happens before" relationship.
However, that's not enough in our case to allow us to mix the users' packages.
Therefore, we'll separate the packages by user.

Here's how we'll handle `create-file-package` messages:

```js
var packagesByUser = {}

function onCreatePackage (msg) {
  // pull variables out of the message
  var author = msg.value.author
  var package = msg.value.content.package

  // validate the content
  if (!package || typeof package !== 'string')
    return console.log('Warning: malformed message', msg)

  // create the user's entry in the listing, if it does not exist yet
  if (!(author in packagesByUser))
    packagesByUser[author] = {}

  // create the package structure (overwrite if it already existed)
  packagesByUser[author][package] = {
    package: package,
    files: {}
  }
}
```

Notice that `msg.value.content.package` is validated, but `msg.value.author` is not.
ssb-server's internal APIs will validate everything in `msg.value.*` except for `msg.value.content.*`.
That's up to the application.

Like incoming HTTP requests, you should always validate the content of the message, as it may be incorrect or harmful.

Let's handle the 'add-file-to-package' message next:

```js
function onAddFile (msg) {
  // pull variables out of the message
  var author = msg.value.author
  var package = msg.value.content.package
  var name = msg.value.content.name
  var fileData = msg.value.content.fileData

  // validate the content
  if (!package || typeof package !== 'string')
    return console.log('Warning: malformed message', msg)
  if (!name || typeof name !== 'string')
    return console.log('Warning: malformed message', msg)
  if (!fileData || typeof fileData !== 'string')
    return console.log('Warning: malformed message', msg)

  // reject if the package doesnt exist yet
  if (!(author in packagesByUser) || !(package in packagesByUser[author]))
    return console.log('Warning: add-file-to-package message published before create-package', msg)

  // update the file entry
  packagesByUser[author][package].files[name] = fileData
}
```

That should be relatively unsurprising.
The remove-file code should also be pretty obvious:

```js
function onRemoveFile (msg) {
  // pull variables out of the message
  var author = msg.value.author
  var package = msg.value.content.package
  var name = msg.value.content.name

  // validate the content
  if (!package || typeof package !== 'string')
    return console.log('Warning: malformed message', msg)
  if (!name || typeof name !== 'string')
    return console.log('Warning: malformed message', msg)

  // reject if the package doesnt exist yet
  if (!(author in packagesByUser) || !(package in packagesByUser[author]))
    return console.log('Warning: add-file-to-package message published before create-package', msg)

  // remove the file entry
  delete packagesByUser[author][package].files[name]
}
```

Now we can tie it together with the processMsg function:

```js
pull(sbot.createLogStream({ live: true }), pull.drain(processMsg))

function processMsg (msg) {
  if (msg.value.content.type == 'create-package')
    onCreatePackage(msg)
  
  if (msg.value.content.type == 'add-file-to-package')
    onAddFile(msg)
  
  if (msg.value.content.type == 'remove-file-from-package')
    onRemoveFile(msg)
}
```

And, there you have it.
Our data-structure will now look like what we expect it to:

```js
// after processing the messages
console.log(packagesByUser) /* => {
  '@hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519': {
    'My Files Package': {
      package: 'My Files Package',
      files: { 'hello-world.txt': 'Hello, world!' }
    }
  }
}
```

But, what about those files in the blob-store?

## Reading Files from Messages

The blob-store provides a hash-id when you add a file, which is used to create [Content-Hash Links](https://ssbc.github.io/docs/ssb/linking.html).

When you expect an attribute to be a link, you can handle it with [ssb-msgs](http://ssbc.github.io/docs/api/ssb-msgs.html) link functions.
Let's create a "get file" function to demonstrate it:

```js
var fs = require('fs')
var mlib = require('ssb-msgs')
var pull = require('pull-stream')
var toPull = require('stream-to-pull-stream')

function writeFile (sbot, user, package, name, outPath) {
  // find the file
  if (!(user in packagesByUser))
    return cb(new Error('not found'))
  if (!(package in packagesByUser[user]))
    return cb(new Error('not found'))
  if (!(name in packagesByUser[user][package].files))
    return cb(new Error('not found'))

  // handle depending on whether it's a link
  var fileData = packagesByUser[user][package].files[name]
  if (mlib.isLink(fileData, 'blob')) {
    // it is, pull from the blob store
    readFileFromBlobstore(sbot, fileData, outPath, cb)
  } else {
    // it's not, the data was inlined in the message
    fs.writeFile(outPath, fileData, cb)
  }
}
function readFileFromBlobstore (sbot, fileData, outPath, cb) {
  // standardize the link format (links can take many different shapes)
  var fileLink = mlib.link(fileData)

  // get from blobstore and write to disk
  pull(
    sbot.blobs.get(fileLink.link),
    toPull.sink(fs.createWriteStream(outpath), cb)
  )
}
```

And there you have it!
A nice quick way to get your jpg:

```js
writeFile(sbot, userId, 'My Files Package', 'my-picture.jpg', './my-picture.jpg', console.log)
```

## Next Steps

From here, you should read about the [Secure Scuttlebutt protocol](https://ssbc.github.io/secure-scuttlebutt/), and be sure to understand the [Content-Hash Linking](https://ssbc.github.io/docs/ssb/linking.html).
There are Howto Guides and Examples along the left nav.
You can also find detailed API references, and some articles, in the [documentation section](https://ssbc.github.io/docs/).

Happy coding!
