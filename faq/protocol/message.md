# What does a message look like?

Here is an example message.
The top level properties are all mandatory, but the user may set anything inside the `content` property, as long as there is a `type` field which is a string between 3 and 64 characters long. 
(The type is up to 64 characters long so that it may be represented by a hash.)

``` js
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

The `previous` is the hash of the message before this in the feed signed by `author`.
`author` is the public key which signs this feed. 
The key pair for this feed *may not* be used for other feeds.
