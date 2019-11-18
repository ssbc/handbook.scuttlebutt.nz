# Create a JS Client

The [ssb-client](https://github.com/ssbc/ssb-client) module can be used for making a connection to a running `ssb-server` process. Internally, it does use some defaults of configuration that at different times and other use cases you may wish to customize, such as the location of the configuration and private keys that it looks up.

```js
var ssbClient = require('ssb-client')
ssbClient(function (err, sbot) {
  // ready
})
```
