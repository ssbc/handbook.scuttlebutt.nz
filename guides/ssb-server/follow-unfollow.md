# Follow / Unfollow

To follow a users feed, publish this `contact` message:

```bash
ssb-server publish --type contact --contact {feedId} --following
```
```js
sbot.publish({ type: 'contact', contact: feedId, following: true }, cb)
```

Scuttlebot will query peers for new messages from this feed.

To stop following a user, publish this `contact` message:

```bash
ssb-server publish --type contact --contact {feedId} --no-following
```
```js
sbot.publish({ type: 'contact', contact: feedId, following: false }, cb)
```
