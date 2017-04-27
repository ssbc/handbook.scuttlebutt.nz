# Modules

> Isaac Schlueter (creator of npm) puts it very well: agreement is very difficult, so limit the amount of agreement necessary.
>
> i.e. write modules.
>
> With less agreement required, it's easier to find points of agreement, and so we can have _more_ agreements overall.

- %88KMgyXpuyF1O1VtKjkycJ+R5j7sJ/DgFwLVAS19J4U=.sha256

## Secure-scuttlebutt vs scuttlebutt vs scuttlebot vs sbot?
#### An explanation of terms, repos and project history

- [`scuttlebutt`](https://github.com/dominictarr/scuttlebutt): a [`gossip protocol`](https://en.wikipedia.org/wiki/Gossip_protocol) that synchronises messages via a vector clock of per-node timestamps or sequences. Dominic got this name from an amazon paper ["Efficient Reconciliation and Flow Control for Anti-Entropy Protocols"](https://www.cs.cornell.edu/home/rvr/papers/flowgossip.pdf). This is the original scuttlebutt module which should now be known as "insecure scuttlebutt". This repo is generally no longer used by the ssb community.

- [`secure-scuttlebutt`](https://github.com/ssbc/secure-scuttlebutt): this is the **database** part of **ssb**. Previously this term referred to the protocol/database as a whole.

- [`scuttlebot`](https://github.com/ssbc/scuttlebot): this repo adds **networking behaviour** to the database (secure-scuttlebutt).

- [`sbot`](https://github.com/ssbc/scuttlebot): short for **scuttlebot**, also the cli command name.

There have been suggestions to rename some repos to better reflect their use and purpose:

secure-scuttlebutt --> [`ssb-db `](https://github.com/ssbc/secure-scuttlebutt/issues/159)
scuttlebot --> [`ssb-server`](https://github.com/ssbc/scuttlebot/issues/378)

## Streams

- [`pull-stream`](https://pull-stream.github.io): minimal composable streams with lazy back pressure and error propagation
- [`mutant`](https://github.com/mmckegg/mutant): lazy observables and reactive html elements

## Modules

- [`depject`](https://github.com/depject/depject): a module system that allows for overlapping opinions

## Database

[`secure-scuttlebutt`](https://github.com/ssbc/secure-scuttlebutt): database of unforgable append-only feeds, optimized for efficient peer-to-peer replication

- [`flumedb`](https://github.com/flumedb/flumedb): modular database where logs are moved with streams
- [`ssb-keys`](https://github.com/ssbc/ssb-keys): keyfile operations for ssb
- [`ssb-feed`](https://github.com/ssbc/ssb-feed): create a secure-scuttlebutt feed
- [`ssb-config`](https://github.com/ssbc/ssb-config): standard configuration for ssb
- [`ssb-ref`](https://github.com/ssbc/ssb-ref): check if a string is a valid ssb-reference

## Crypto

- [`secret-handshake`](https://github.com/auditdrivencrypto/secret-handshake): secure-channel based on a a mutually authenticating key agreement handshake, with forward secure identity metadata.
- [`private-box`](https://github.com/auditdrivencrypto/private-box): private message between two parties (with no `to` field)

## Server

[`scuttlebot`](https://github.com/ssbc/scuttlebot): peer-to-peer log store used as a database, identity provider, and messaging system

- [`muxrpc`](https://github.com/ssbc/muxrpc): lightweight multiplexed rpc
- [`mdmanifest`](https://github.com/ssbc/mdmanifest): markdown manifests for mux rpc apis
- [`muxrpcli`](https://github.com/ssbc/muxrpcli): command-line interface to mux rpc servers
- [`secret-stack`](https://github.com/ssbc/secret-stack): connect peers to each other using secret-handshakes
- [`ssb-query`](https://github.com/dominictarr/ssb-query): a functional query engine, that operates over streams of js objects, and can be optimized via database indexes.
- [`ssb-blobs`](https://github.com/ssbc/ssb-blobs): blob gossiping ssb-subprotocol
- [`multiblob`](https://github.com/dominictarr/multiblob): a content-addressable-store that supports multiple hashing algorithms
- [`ssb-ebt`](https://github.com/ssbc/ssb-ebt): replication with epidemic-broadcast-trees
- [`easy-ssb-pub`](https://github.com/staltz/easy-ssb-pub): an easy-to-host server that runs an SSB "Pub"

## Client

- [`patchcore`](https://github.com/ssbc/patchcore): a shared library to build ssb apps
- [`ssb-client`](https://github.com/ssbc/ssb-client): client library to scuttlebot
- [`ssb-party`](https://git.scuttlebot.io/%25bS%2FWGqQrhQfH8eoyWieK%2B9M56DjJ8Q4ulkvb6sXZwPo%3D.sha256): get a scuttlebot client instance. if scuttlebot isn't running, start it in the background, and keep it running until all the clients have disconnected.
- [`ssb-notifier`](https://github.com/ssbc/ssb-notifier): desktop notifications for secure-scuttlebutt activity
- [`ssb-avatar`](https://github.com/dominictarr/ssb-avatar): query for the avatar that an ssb feed has been assigned
- [`ssb-mentions`](https://github.com/dominictarr/ssb-mentions): extract the mentions in a ssb message
- [`ssb-markdown`](https://github.com/ssbc/ssb-markdown): render ssb messages to markdown.
- [`ssb-sort`](https://github.com/ssbc/ssb-sort): sort a collection of messages by their causal order

## Git

- [`git-ssb`](https://git.scuttlebot.io/%25n92DiQh7ietE%2BR%2BX%2FI403LQoyf2DtR3WQfCkDKlheQU%3D.sha256): Git repos, issue tracking, and pull requests using SSB
  - [`git-remote-ssb`](https://git.scuttlebot.io/%25ZVTOK3GA2aewEDI2rPxJqKXEIv4OIUN2swMPE2FeJm8%3D.sha256): A git remote helper for using `ssb://` URLs with git
  - [`git-ssb-web`](https://git.scuttlebot.io/%25q5d5Du%2B9WkaSdjc8aJPZm%2BjMrqgo0tmfR%2BRcX5ZZ6H4%3D.sha256): A web server for browsing repos locally
