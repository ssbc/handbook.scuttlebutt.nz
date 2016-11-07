# Message

> Patchwork is one particular interpretation of the ssb protocol. using patchwork you click buttons and type into fields and patchwork creates cryptographic messages which are replicated over ssb. These interpretations are _subjective_, currently, when I clicked "follow" on your account patchwork created a message that looked like `{type: 'contact', contact: @dust , following: true}`. currently, ssb reacts to that, and if someone I "follow" follows someone else, I replicate that someone else too, making their data more available. This is considered a favor to that feed, and the friend who followed.
> You can change this sort of behavior without changing the wire protocol. Clients could publish whatever they want, and interpret another message however they want. The meaning is created when two peers have the same interpretation. You don't get to choose how someone interprets you, but you may choose how you interpret them. Lets call this "freedom of interpretation"?

- %RqH7UzDJNhKbu+LNGIe9eRrbSIGTybVb1ZZ6n+593tc=.sha256

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
