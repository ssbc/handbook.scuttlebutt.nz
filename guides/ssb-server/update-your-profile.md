# Update your Profile

## Name

To name yourself, publish this `about` message:

```bash
ssb-server publish --type about --about {yourId} --name {name}
```
```js
sbot.publish({type: 'about', about: yourId, name: name}, cb)
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
