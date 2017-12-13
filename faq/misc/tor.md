# How can I preserve my privacy

Scuttlebutt does not require to use your real name. You can use
whatever you like. Connecting to other peers to exchange gossip
messages will reveal your IP and might be used to de-anonymize
you. 

Luckily scuttlebutt has built in support for
[TOR](https://torproject.org/). You need to be running the TOR daemon
for scuttlebutt to relay messages through the onion network. If you
want secure scuttlebutt to ONLY connect to other TOR nodes, you need
to pass a –tor-only flag when running sbot.

You can find a list pubs available over TOR at the
[wiki](https://github.com/ssbc/scuttlebot/wiki/Pub-Servers). Please
note that you might need to contact the person running it for an
invite.

Please note this is not an easy way to game the system or spam
it. Scuttlebutt already has a great system for blocking users.

Please note that even when using TOR the (normal
rules)[https://www.whonix.org/wiki/DoNot] for staying anonymous still
applies though.
