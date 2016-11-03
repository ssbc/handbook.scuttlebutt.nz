# Private Message

For private sharing, Scuttlebot uses [libsodium](http://doc.libsodium.org/) to encrypt confidential log-entries. Feed IDs are public keys, and so once two feeds are mutually following each other, they can exchange confidential data freely.

Private-box is a format for encrypting a private message to many parties. It is designed according to the [audit-driven crypto design process](https://github.com/crypto-browserify/crypto-browserify/issues/128). You can find the repository on at [github:dominictarr/private-box](https://github.com/auditdrivencrypto/private-box)
