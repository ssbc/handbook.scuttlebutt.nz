# Announce a Pub Server

To announce a pub server, publish this `pub` message:

```bash
ssb-server publish --type pub --address.key {feedId} --address.host {string} --address.port {number}
```
```js
sbot.publish({ type: 'pub', address: { key: feedId, host: string, port: number } }, cb)
```

Scuttlebot, and any user that follows you, will add the pub to their peer list, and begin contacting it for syncing.
