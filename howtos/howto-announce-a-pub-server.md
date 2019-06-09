# Announce a Pub Server

To announce a pub server, publish this `pub` message:

```bash
sbot publish --type pub --pub.link {feedId} --pub.host {string} --pub.port {number}
```
```js
sbot.publish({ type: 'pub', pub: { link: feedId, host: string, port: number } }, cb)
```

Scuttlebot, and any user that follows you, will add the pub to their peer list, and begin contacting it for syncing.