# Message

Each message contains:

- A signature
- The signing public key
- A content-hash of the previous message
- A sequence number
- A timestamp
- An identifier of the hashing algorithm in use (currently only "sha256" is supported)
- A content object

Here's an example message:

```
{
  "previous": "%26AC+gU0t74jRGVeDY013cVghlZRc0nfUAnMnutGGHM=.sha256",
  "author": "@hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519",
  "sequence": 216,
  "timestamp": 1442590513298,
  "hash": "sha256",
  "content": {
    "type": "vote",
    "vote": {
      "link": "%WbQ4dq0m/zu5jxll9zUbe0iGmDOajCx1ZkLKjZ80JvI=.sha256",
      "value": 1
    }
  },
  "signature": "Sjq1C3yiKdmi1TWvNqxIk1ZQBf4pPJYl0HHRDVf/xjm5tWJHBaW4kXo6mHPcUMbJYUtc03IvPwVqB+BMnBgmAQ==.sig.ed25519"
}
```
