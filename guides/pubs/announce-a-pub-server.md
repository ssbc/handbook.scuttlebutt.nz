# Announce a Pub Server

To announce a pub server, publish this `pub` message, replacing the parts in quotes with your pub server's values:

```bash
ssb-server publish --type pub --address.key "@myPubId.ed25519" --address.host "awesomepub.mydomain.org" --address.port 8008
```

You can achieve the same from JavaScript like such:
```js
sbot.publish({ type: 'pub', address: { key: pubId, host: string, port: number } }, cb)
```

`ssb-server`, and any user that follows you, will add the pub to their peer list, and begin contacting it for syncing.

If you do this correctly, the newest message of your pub should look like this:

```terminal
$ ssb-server getLatest '@myPubId=.ed25519' | jq '.value.content'
{
  "type": "pub",
  "address": {
    "key": "@myPubId.ed25519",
    "host": "awesomepub.mydomain.org",
    "port": 8008
}
```
