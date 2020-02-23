# Update your Profile

There are three major recognised `about` fields: "name", "description" and "image". The following describes how to set all three.

## Name and Description (bio)

To name yourself, publish this `about` message:

```bash
ssb-server publish --type about --about {yourId} --name {name}
```
```js
sbot.publish({type: 'about', about: yourId, name: name}, cb)
```

To provide a "bio" or description, publish this `about` message:

```bash
ssb-server publish --type about --about {yourId} --description {description}
```
```js
sbot.publish({type: 'about', about: yourId, description: description}, cb)
```

To combine both together, publish this `about` message:

```bash
ssb-server publish --type about --about {yourId} --name {name} --description {description}
```
```js
sbot.publish({type: 'about', about: yourId, name: name, description: description}, cb)
```

For example:

```bash
ssb-server publish --type about --about $(ssb-server whoami | grep '"id"' | cut -d\" -f4) --name "Some Server" --description "I'm just this server, running [ssb-server](https://github.com/ssbc/ssb-server) don'tcha know?"
```

## Picture

To set your picture, first [add the image to the blobstore](publish-a-file.md).
Then, publish this `about` message:

```bash
ssb-server publish --type about --about {yourId} --image {fileId}
```
```js
sbot.publish({type: 'about', about: yourId, image: fileId}, cb)
```
