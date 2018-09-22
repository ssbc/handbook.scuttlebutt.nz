# Modules

> Isaac Schlueter (creator of npm) puts it very well: agreement is very difficult, so limit the amount of agreement necessary.
>
> i.e. write modules.
>
> With less agreement required, it's easier to find points of agreement, and so we can have _more_ agreements overall.

- %88KMgyXpuyF1O1VtKjkycJ+R5j7sJ/DgFwLVAS19J4U=.sha256

## Streams

- [`pull-stream`](https://pull-stream.github.io): minimal composable streams with lazy back pressure and error propagation
- [`mutant`](https://github.com/mmckegg/mutant): lazy observables and reactive html elements

## Modules

- [`depject`](https://github.com/depject/depject): a module system that allows for overlapping opinions
- [`depnest`](https://www.npmjs.com/package/depnest): commonly used depject helper

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
- pubs
  - [`easy-ssb-pub`](https://github.com/staltz/easy-ssb-pub): an easy-to-host server that runs an SSB "Pub"
  - [`ssb-pub`](https://github.com/ahdinosaur/ssb-pub): easily host your own ssb pub in a docker container

## Client

- [`patchcore`](https://github.com/ssbc/patchcore): a shared library to build ssb apps
- [`ssb-client`](https://github.com/ssbc/ssb-client): client library to scuttlebot
- [`ssb-party`](https://git.scuttlebot.io/%25bS%2FWGqQrhQfH8eoyWieK%2B9M56DjJ8Q4ulkvb6sXZwPo%3D.sha256): get a scuttlebot client instance. if scuttlebot isn't running, start it in the background, and keep it running until all the clients have disconnected.
- [`ssb-notifier`](https://github.com/ssbc/ssb-notifier): desktop notifications for secure-scuttlebutt activity
- [`ssb-avatar`](https://github.com/dominictarr/ssb-avatar): query for the avatar that an ssb feed has been assigned
- [`ssb-mentions`](https://github.com/dominictarr/ssb-mentions): extract the mentions in a ssb message
- [`ssb-markdown`](https://github.com/ssbc/ssb-markdown): render ssb messages to markdown.
- [`ssb-sort`](https://github.com/ssbc/ssb-sort): sort a collection of messages by their causal order

## Mobile

- [`react-native-node`](https://github.com/staltz/react-native-node): Node.js background process for React Native apps, fundamental for running sbot on mobile devices
- [`react-native-ssb-shims`](https://github.com/ssbc/react-native-ssb-shims): basic shims required to insert modules from the SSB ecosystem into React Native apps
- [`react-native-scuttlebot`](https://github.com/ssbc/react-native-scuttlebot): scuttlebot but for React Native applications
- [`react-native-ssb-client`](https://github.com/ssbc/react-native-ssb-client): like ssb-client, but runs in React Native apps
- [`react-native-ssb-client-keys`](https://github.com/ssbc/react-native-ssb-client-keys): keyfile operations for SSB, to be used from the client-side of React Native apps

## Git

- [`git-ssb`](https://git.scuttlebot.io/%25n92DiQh7ietE%2BR%2BX%2FI403LQoyf2DtR3WQfCkDKlheQU%3D.sha256): Git repos, issue tracking, and pull requests using SSB
  - [`git-remote-ssb`](https://git.scuttlebot.io/%25ZVTOK3GA2aewEDI2rPxJqKXEIv4OIUN2swMPE2FeJm8%3D.sha256): A git remote helper for using `ssb://` URLs with git
  - [`git-ssb-web`](https://git.scuttlebot.io/%25q5d5Du%2B9WkaSdjc8aJPZm%2BjMrqgo0tmfR%2BRcX5ZZ6H4%3D.sha256): A web server for browsing repos locally

## App helpers

- [`scuttle-shell`]()
- [`scuttle-poll`]()
- [`scuttle-gathering`]()
- [`scuttle-tag`](https://github.com/ssbc/scuttle-tag): Tag reading and manipulation plugin for secure scuttlebutt.
- [`scuttle-blog`](https://github.com/ssbc/scuttle-blog): A helper module which covers all your ssb blog related needs from `blog` data
- [`ssb-chat-core`](https://github.com/stripedpajamas/ssb-chat-core): All the core functionality used by [`scat`](./applications.md#scat)
