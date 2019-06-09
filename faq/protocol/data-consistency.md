# How do you ensure data consistency between users?

Sometimes, you want to make sure that other users are aware of a given change.
This can be implemented by posting acknowledgement messages.

There is also active discussion about using signed pings to send ephemeral acknowledgements (off of the feeds).

## Is SSB highly available (AP) or highly consistent (CP)?

SSB is highly-available (AP).
Devices can create messages while offline, then synchronize later.
This means all data is eventually-consistent.

## Can I know if I have the latest messages from somebody?

No, because it's possible for devices to drop and continue operating (a network "partition").
There's a proposal to used signed pings to measure the "freshness" of a feed, but this could only be used in small groups of interested peers.

## Is there a global total order in SSB?

No.
There is, however, a global [partial order](http://en.wikipedia.org/wiki/Partially_ordered_set#Formal_definition).

An individual feed has an internal [total order](http://en.wikipedia.org/wiki/Total_order).
Every message contains a sequence number and a pointer to the previous message in that feed.

If feed A posts a message that links to a message in feed B, then we know that A's message is *after* B's.
That is, message-links imply a `happens-before` relationship.
(This is because, in order to know the hash of an object, that object must already exist.)

Messages contain [monotonically increasing](http://en.wikipedia.org/wiki/Monotonic_function) UTC timestamps and sequence numbers.
This means you can assign an order to any two messages.
However, be aware that there is no way to ensure that the timestamp is accurate.
