# Concepts

![Hermies watering](/assets/garden/hermies-watering.gif)

This section is a collection of concepts that are useful to understand the scuttleverse.

A lot of these are common to many of the current p2p database protocols, however there are important differences to keep in mind.

## Network Topology

> twitter implements a social network (decentralized network of friends and influencers) on a computer network with a different topology (data center hub and user spokes)
>
> Twister implements a social network (again, dexnet of friends & followors) on a uniformly distributed decentralized network, user feeds distributed across a DHT (distributed hash table) and a blockchain (for user names) - twister is decentralized, but it's uniformly decentralized, each peer puts in roughly the same commitment of resources, which sounds like a good thing, sure.
But this means that twister is a decentralized implementation of a centralized idea, and thus conceputallly centralized.
>
> But secure-scuttlebutt is different, it maps a the social network on to a computer network that is essentially the same topology! that is, the connections between humans maps approximately to the the connections between computers. if you follow someone, you really actually follow them at the data layer.
>
> I feel this means the user experience is in harmony with the architecture of the system.
>
> I can't fairly claim that ssb isn't conceputally centralized right now, because there is only a small number of developers, but there is nothing in the architecture that prevents having many implementations - so if we succeed, I think that will happen.

- %lmELhGVLXcWrygyG0whgkzkmjlmiB1jZf5EshQ5zfhs=.sha256

> bittorrent/DAT like protocols are pretty good for moving heavy data. (video, OS images, etc) the best part is that you collaborate only with other peers who are invested in a particular dataset.
>
> But the weakness (in my opinion) is that they rely on a DHT.
> DHTs are bad because peers collaborate anonymously, you have cannot estimate their trustworthyness and consequently, DHTs tend to have poor privacy (because an adversary could easily add peers that monitor you) and poor sybil resistance (again, because you have no way to know that a peer is "near you" or "on your side")
>
> This happens because work is distributed between peers uniformly.
> Peers are mapped into a hash ring, so to get a hash, you traverse peers closer and closer to your target.
>
> One of the core ideas in ssb is to map the computer network along the social network (thus defeating spam, because you arn't friends with spammers)

- %0asWjhFa51ri/OOSXJgC/aUweNzhxHi2/7+PXhwUzH8=.sha256

## Permissions

> secure-scuttlebutt absolutely aims to grow into a pretty good decentralized database,
> but because it's _decentralized_ that means it's gonna turn out pretty different to say, mysql.
>
> The fundamental difference being that in a decentralized database, "permissions" are enforced by the reader, not the writer (or rather, receiver of the write - "the database")

- %qn9zPU/d8021Cpv5/t7FFZv8eoUUDDOJ8xdhor5w+bA=.sha256

> This is the thing which is fundamentally different with this decentralized architecture than with centralized. In a centralized database, the database is the point of control. Who has permission to write what is determined by the database. In this decentralized architecture, if you want to write something, just write it. the other clients will decide whether that write was valid, and accept or ignore it.

- %KSSrusb3gQsRe6d3ZkKfiQTrGWM7OB1ePNEh6yzsA8I=.sha256
