# Private Message

For private sharing, Scuttlebot uses [libsodium](http://doc.libsodium.org/) to encrypt confidential log-entries. Feed IDs are public keys, and so once two feeds are mutually following each other, they can exchange confidential data freely.

Private-box is a format for encrypting a private message to many parties. It is designed according to the [audit-driven crypto design process](https://github.com/crypto-browserify/crypto-browserify/issues/128). You can find the repository on at [github:dominictarr/private-box](https://github.com/auditdrivencrypto/private-box)

> When you want a message to be private, it is encrypted end-to-end with private-box
So gossipers will still see the cyphertext of your message, but will not see the plaintext. best of all, the recipients (including the number of recipient!) is also encrypted, so a patchwork private message leakes much less metadata than GPG. (it's obviously a message for someone in the network, but there is no clues who*)
>
> * Excepting timing information. To obsecure timing information, you'd post messages randomly and relay encrypted sends. Doable, but quite a niche, will leave this for later, once more people are using the system.
