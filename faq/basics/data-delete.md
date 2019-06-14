# Is it possible to delete or edit messages?

---

Secure Scuttlebutt is immutable, so strictly speaking you cannot change anything that has been published.
There are, however, abstractions on top of the feeds which allow behaviors like deletion and editing.

## Delete

A true delete is not possible: instead, you post a message asking your friends to _ignore_ the message.
This is somewhat like real life - if you say something embarrassing, the best you can do is ask your friends to ignore it.
(Life is much better when you have good friends.)

## Edit

Editable objects can be represented by posting a create message, and then posting a message that refers to that message and overrides properties on that message, or applies patches to it.
By declaring lists of who may or may not edit documents, and using CRDTs to ensure convergence, you could implement access controls.
