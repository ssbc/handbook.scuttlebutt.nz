# Gossip

In Scuttlebutt, 3rd parties can relay (gossip) information for you, which improves availability.

Every message is signed, so gossipers cannot interfer with the message - note this is significantly different than real world gossip! _secure_ gossip if you will.

[![GOSSIP PHONE](../assets/gossip-phone.jpg)](https://twitter.com/BatLabels/status/700324774833217536)

## Following 

Users choose which [feeds](./feed.html) to synchronize by following them.

Presently, Scuttlebot's replicate plugin, which is enabled by default, looks on the master user's feed for `type: contact` messages to know which users are currently followed.

## Replication

Since feeds are append-only, gossip is simple: request all messages in the feed that are newer than the latest message you know about. Scuttlebot maintains a table of known peers, which it cycles through, asking for updates for all followed feeds.

Since the messages are always signed, information can be distributed in any way, such as through a [sneakernet](https://en.wikipedia.org/wiki/Sneakernet). For example, you could put the latest gossip on an SD card and send it to your friend via [pigeon post](https://en.wikipedia.org/wiki/Pigeon_post).

## Network

The protocol creates a [global gossip network](https://en.wikipedia.org/wiki/Gossip_protocol). This means that information is able to distribute across multiple machines, without requiring direct connections between them.

![Gossip graph 1](../assets/gossip-graph1.png)

Even though Alice and Dan lack a direct connection, they can still exchange feeds:

![Gossip graph 2](../assets/gossip-graph2.png)

This is because gossip creates "transitive" connections between computers. Dan's messages travel through Carla and the Pub to reach Alice, and visa-versa.
