# How can I preserve my privacy

## Pick a safe name

Scuttlebutt does not require to use your real name. You can use
whatever you like. If you want to stay a bit more private, choose a name that
people wouldn't normally associate with you.

## Keep it in the Scuttleverse

Scuttlebutt has a way of indicating to public gateways (places that show scuttlebutt
messages on the web like viewer.scuttlebutt.io ) that you don't want anything
you say to show up there.

To do this, open up your Terminal app and type the following (with `<YOURID>`
replaced with your actual ID).

```
sbot publish --type about --about "<YOURID>" --no-publicWebHosting
```

If you ever want to re-enable it you can say

```
sbot publish --type about --about "<YOURID>" --publicWebHosting
```

## Need more? 

Connecting to other peers to exchange gossip
messages will reveal your IP and might be used to de-anonymize
you. Luckily scuttlebutt has built in support for
[TOR](https://torproject.org/). See the [tor page](tor.md) for more details.

