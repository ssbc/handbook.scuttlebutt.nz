# Why is there a size limit on messages?

---

Messages are limited at 8kb in size so that the time required to replicate is predictable.
Also, since peers will replicate all messages for peers they follow, it's important that peers do not create an unreasonable amount of work for each other.

If you need a larger object, use "blob attachments."
