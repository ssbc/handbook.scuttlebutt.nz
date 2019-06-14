# What are attachments?

---

Attachments are immutable blobs of binary data, similar to email attachments.
When clients see a message that refers to a given attachment, it will request it if the attachment isn't already stored locally.
Attachments are limited to 10mb.

Replication of larger files could be implemented by integrating bittorrent (or even better, [webtorrent](https://github.com/feross/webtorrent)).
