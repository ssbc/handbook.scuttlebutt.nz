# Can I use Scuttlebutt with Tor?

Scuttlebutt has built in support for
[Tor](https://torproject.org/). You need to be running the TOR daemon
for scuttlebutt to relay messages through the onion network. If you
want secure scuttlebutt to ONLY connect to other Tor nodes, you need
to pass a `–tor-only` flag when running sbot.

You can find a list pubs available over Tor at the
[wiki](https://github.com/ssbc/scuttlebot/wiki/Pub-Servers). Please
note that you might need to contact the person running it for an
invite.

Please note this is not an easy way to abuse or spam
people. Scuttlebutt already has a great system for blocking users.

Please note that even when using Tor, the [normal
rules](https://www.whonix.org/wiki/DoNot) for staying anonymous still
applies though.

# What other cool things can I do with Tor?

Glad you asked.

If you configure Tor as a hidden service and redirect port 8008 to
localhost 8008 then your sbot service will be available over Tor. Add
the following to `/etc/tor/torrc`:

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8008 127.0.0.1:8008
```

And reload Tor, then your onion address will be available in
`/var/lib/tor/hidden_service/hostname`.

Besides hiding your IP and doing end-to-end encryption, Tor also does
location transparency. Meaning your hostname will always stay the same
no matter where you are connected, and anyone can connect to you
directly. No need to open ports in your firewall!

This means that its possible to do p2p connections without pubs and
talk direcly to your friends. If you create an invite from your
machine (you probably need to add `"allowPrivate": true` in `/.ssb/config`),
replace the ip or hostname with your onion adress and send that to a
friend. They will be able to connect directly to you and start
receiving messages straight away, assuming your machine is online and running 
of course.
