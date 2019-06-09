# Secure-scuttlebutt vs scuttlebutt vs scuttlebot vs sbot?

---

## An explanation of terms, repos and project history

- [`scuttlebutt`](https://github.com/dominictarr/scuttlebutt): a [`gossip protocol`](https://en.wikipedia.org/wiki/Gossip_protocol) that synchronises messages via a vector clock of per-node timestamps or sequences. Dominic got this name from an amazon paper ["Efficient Reconciliation and Flow Control for Anti-Entropy Protocols"](https://www.cs.cornell.edu/home/rvr/papers/flowgossip.pdf). This is the original scuttlebutt module which should now be known as "insecure scuttlebutt". This repo is generally no longer used by the ssb community.

- [`ssb-db`](https://github.com/ssbc/secure-scuttlebutt): this is the **database** part of **ssb**. Previously this term referred to the protocol/database as a whole.

- [`ssb-server`](https://github.com/ssbc/ssb-server): this repo adds **networking behaviour** to the database (secure-scuttlebutt).

- [`sbot`](https://github.com/ssbc/ssb-server): short for **scuttlebot**, previously the CLI command name to control `ssb-server`. Now also named `ssb-server`.

## Old Names

The following components of the Scuttlebutt reference implementation have been renamed:

- `secure-scuttlebutt` --> [`ssb-db`](https://github.com/ssbc/ssb-db/issues/159)
- `scuttlebot` --> [`ssb-server`](https://github.com/ssbc/ssb-server/issues/378)
