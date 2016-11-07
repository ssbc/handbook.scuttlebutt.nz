# modules

## streams

[`pull-stream`](https://github.com/pull-stream/pull-stream): minimal composable streams with lazy back pressure and error propagation

see more at [pull-stream.github.io](https://pull-stream.github.io)

## database

[`secure-scuttlebutt`](https://github.com/ssbc/secure-scuttlebutt): database of unforgable append-only feeds, optimized for efficient peer-to-peer replication

- [`ssb-keys`](https://github.com/ssbc/ssb-keys): keyfile operations for ssb
- [`ssb-feed`](https://github.com/ssbc/ssb-feed): create a secure-scuttlebutt feed
- [`ssb-config`](https://github.com/ssbc/ssb-config): standard configuration for ssb
- [`ssb-ref`](https://github.com/ssbc/ssb-ref): check if a string is a valid ssb-reference
- [`ssb-blobs`](https://github.com/ssbc/ssb-blobs): blob gossiping ssb-subprotocol
- [`multiblob`](https://github.com/dominictarr/multiblob): a content-addressable-store that supports multiple hashing algorithms
- [`map-filter-reduce`](https://github.com/dominictarr/map-filter-reduce): A functional query engine, that operates over streams of js objects, and can be optimized via database indexes.

## crypto

- [`secret-handshake`](https://github.com/auditdrivencrypto/secret-handshake): secure-channel based on a a mutually authenticating key agreement handshake, with forward secure identity metadata.
- [`private-box`](https://github.com/auditdrivencrypto/private-box): private message between two parties (with no `to` field)

## server

[`scuttlebot`](https://github.com/ssbc/scuttlebot): peer-to-peer log store used as a database, identity provider, and messaging system

- [`muxrpc`](https://github.com/ssbc/muxrpc): lightweight multiplexed rpc
- [`mdmanifest`](https://github.com/ssbc/mdmanifest): markdown manifests for mux rpc apis
- [`muxrpcli`](https://github.com/ssbc/muxrpcli): command-line interface to mux rpc servers
- [`secret-stack`](https://github.com/ssbc/secret-stack): connect peers to each other using secret-handshakes

## client

- [`ssb-notifier`](https://github.com/ssbc/ssb-notifier): desktop notifications for secure-scuttlebutt activity
- [`ssb-client`](https://github.com/ssbc/ssb-client): client library to scuttlebot
- [`ssb-avatar`](https://github.com/dominictarr/ssb-avatar): query for the avatar that an ssb feed has been assigned
- [`ssb-mentions`](https://github.com/dominictarr/ssb-mentions): extract the mentions in a ssb message
- [`ssb-markdown`](https://github.com/ssbc/ssb-markdown): render ssb messages to markdown.
- [`ssb-sort`](https://github.com/ssbc/ssb-sort): sort a collection of messages by their causal order
