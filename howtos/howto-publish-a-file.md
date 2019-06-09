# Publish a File

The blobs plugin gives you access to a content-addressed files database.
[Here is the API](../api/scuttlebot-blobs.md).

```bash
$ echo "hello, world" | sbot blobs.add
&hT/5N2Kgbdv3IsTr6d3WbY9j3a6pf1IcPswg2nyXYCA=.sha256
$ sbot blobs.get "&hT/5N2Kgbdv3IsTr6d3WbY9j3a6pf1IcPswg2nyXYCA=.sha256"
hello, world
```
```js
pull(
  pull.values('hello, world'),
  sbot.blobs.add(function (err, hash) {
    pull(sbot.blobs.get(hash), pull.collect(function (err, values) {
      if (err) throw err
      assert(values.join('') == 'hello, world')
    }))
  })
)
```

After adding a file to the blobstore, you can mention the file in a post to publish it.
When peers receive your message, they'll see the file reference (if they can decrypt the message) and sync the file using the blobs api.

```bash
sbot publish --type post --text "checkout this pic! ![CHC.jpg](&akkg6hKV7ee6sATu3mLeR6KfhgUbNGHWl/QJeALpQ0Y=.sha256)" --mentions.0.name CHC.jpg --mentions.0.link &akkg6hKV7ee6sATu3mLeR6KfhgUbNGHWl/QJeALpQ0Y=.sha256 --mentions.0.size 288388 --mentions.0.type image/jpeg
```
```js
sbot.publish({
  type: 'post',
  text: 'checkout this pic! ![CHC.jpg](&akkg6hKV7ee6sATu3mLeR6KfhgUbNGHWl/QJeALpQ0Y=.sha256)',
  mentions: [{
    name: 'CHC.jpg',
    link: '&akkg6hKV7ee6sATu3mLeR6KfhgUbNGHWl/QJeALpQ0Y=.sha256',
    size: 288388,
    type: 'image/jpeg'
  }]
}, cb)
```

## Limitations

It's best not to post files larger than 5MB right now, and to avoid flooding a lot of files.
Peers that follow you will automatically sync files that you reference in your posts, without the user asking first.
If you abuse that power, you'll get unfollowed!