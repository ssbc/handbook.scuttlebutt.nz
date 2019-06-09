# Why do you have pub servers? isn't that a point of centralization?

---

Routers with Network Address Translation ("NAT") and firewalls, and the shortage of IP addresses, make p2p difficult.
The simplest way around this problem was to create "pub servers".

A pub server is exactly like a normal client, except you run it on a server with a static IP address.
It's a "pub" as in a bar where your friends meet to exchange gossip.

Anyone can run a pub server.
It's not centralization because pub servers are totally generic (same code as "clients") and because, if we did have ipv6 and full p2p, ssb would work without any changes.
Also note that ssb also detects other peers running on your local network (wifi) and connects to them directly, without pub servers.
