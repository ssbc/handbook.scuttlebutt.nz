# Create a JS Client

The current process for connecting to Scuttlebot involves loading the master keypair from sbot's config (`~/.ssb/secret`).
Do this automatically with the [ssb-client](https://github.com/ssbc/ssb-client) module.

```js
var ssbClient = require('ssb-client')
ssbClient(function (err, sbot) {
  // ready
})
```