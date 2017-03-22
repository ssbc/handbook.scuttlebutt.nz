# Design Challenge: Avoid Centralization and Singletons

SecureScuttlebutt goes out of its way to avoid both centralization and singletons.

## Avoiding Centralization

The danger of centralization is obvious: it creates a single point of failure that can easily be attacked, or act as an attacker.
And, it creates a monoculture of information, as the central point starts to control [what information is trusted, or ranked highly](using-trust-in-open-networks.md).

To avoid centralization, you make every peer the same.

Due to limitations inherent in the modern Internet, this is hard to do.
Home routers perform Network Address Translation to make a single IP address behave like many, which makes it simple to make outgoing connections, but difficult to receive incoming connections.

Most networked applications, including SSB, solve this by connecting to publicly addressable servers.
Sometimes P2P systems use clever techniques ([TURN](http://en.wikipedia.org/wiki/Traversal_Using_Relays_around_NAT), [STUN](http://en.wikipedia.org/wiki/STUN), [ICE](http://en.wikipedia.org/wiki/Interactive_Connectivity_Establishment)) to reduce the role of the servers, but it's still necessary to have them.


SSB uses the so-called "Pub" servers to rehost the feeds and blobs of the users, which has the added benefit of improving network availability (two peers don't need to be online at the same time to exchange messages).
However, amongst the community, they're considered a centralization risk.

We mitigate the risk by avoiding putting any special authority or trust in the Pubs.
Users may be hosted by many pubs at once, and can change pubs without losing the data or identity.
A pub server may go down, and others will still provide service.

Contrast this with email servers, which are ostensibly decentralized (you may run your own email server) but you must have *exactly one* email server, and if it is down you will not receive email, which makes running your own email server a considerable hassle (not to mention handling spam).

## Avoiding Singletons

SecureScuttlebutt also avoids P2P structures that represent singletons - specifically, it avoids using a [Distributed Hash Table](http://en.wikipedia.org/wiki/Distributed_hash_table) or a [global blockchain](http://en.wikipedia.org/wiki/Bitcoin#Block_chain).

SSB avoids P2P singletons partially to show that it can be done (most P2P designs use DHT or global blockchains) and also because those are just P2P versions of centralized systems.
Social Networks are already constructed around a decentralized experience.
Popular social networks (fb, twitter) have centralized implementations, but you use them to interact with your _peers_, so on that level they are P2P.

SecureScuttlebutt takes this decentralized experience and maps the networking layer (the key part of the implementation) on top of the decentralized human/user network.
It would be a shame to go to all that trouble to decentralize, but then adopt a singleton.
Also, global blockchains are heavy (require nodes to store entire chain, and to waste CPU power) and DHTs are susceptible to spam.
These structures also both make the network unprivate, by making all information available globally.

That said, like any good tool, SSB has been built to interoperate with other programs.
Though it's important to us that core remain viable without singletons, the community is free to add protocols wherever they see fit, and is encouraged to do so.
