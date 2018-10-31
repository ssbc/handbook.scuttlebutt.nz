# How can I preserve my privacy

## Don't use your real name

Scuttlebutt does not require to use your real name. You can use
whatever you like. If you want to stay a bit more private, choose a name that 
people wouldn't normally associate with you. This is known as a [handle](https://en.wikipedia.org/wiki/User_(computing)).

## Keep it in the Scuttleverse

Scuttlebutt has a way of indicating to public gateways (places that mirror Scuttlebutt
content onto the old web such as the volunteer run [viewer.scuttlebutt.io](https://viewer.scuttlebot.io)) that you don't want anything you say to show up there. This opt-out is enabled by default when installing Scuttlebutt using the [Patchwork](https://github.com/ssbc/patchwork) client.

To do this globally for all client, open up your Terminal app and type the following (with `<YOURID>`
replaced with your actual ID).

```
sbot publish --type about --about "<YOURID>" --no-publicWebHosting
```

If you ever want to re-enable it you can say

```
sbot publish --type about --about "<YOURID>" --publicWebHosting
```

## Use Tor to cloak your location
Connecting in a peer to peer manner to exchange gossip messages will reveal your [IP adddress](https://en.wikipedia.org/wiki/IP_address) to other peers which could be be used to de-anonymize you. Luckily, Scuttlebutt has built in support for
[Tor](https://torproject.org/). See the [SSB handbook page on Tor](tor.md) for more details.

