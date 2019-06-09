# Get your Address

To get your address:

```bash
ssb-server getAddress
```
```js
sbot.getAddress(cb)
```

Addresses look like `ip:port:id`.
This will try to get your public address.
If you don't have a public IP, this will probably give an IP in the 192 range.
