# How does user identity work?

Users are identified by public keys.
This means it is not necessary to have a global registry of user names, nor to have a central server that tracks the action of users.
Instead, every user action (post) is signed, and this can be verified by any peer.

To evaluate the trustworthiness of a user, you look at information published by other trusted users about the target.
If trusted users have flagged the target, then it is a bad actor.
If trusted users have followed the target, then it is probably a good actor.
