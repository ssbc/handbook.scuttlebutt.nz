# Private Message

For private sharing, Scuttlebot uses [libsodium](http://doc.libsodium.org/) to encrypt confidential log-entries. Feed IDs are public keys, and so once two feeds are mutually following each other, they can exchange confidential data freely.

Private-box is a format for encrypting a private message to many parties. It is designed according to the [audit-driven crypto design process](https://github.com/crypto-browserify/crypto-browserify/issues/128). You can find the repository on at [github:dominictarr/private-box](https://github.com/auditdrivencrypto/private-box)

> When you want a message to be private, it is encrypted end-to-end with private-box
So gossipers will still see the cyphertext of your message, but will not see the plaintext. best of all, the recipients (including the number of recipient!) is also encrypted, so a patchwork private message leakes much less metadata than GPG. (it's obviously a message for someone in the network, but there is no clues who*)
>
> * Excepting timing information. To obsecure timing information, you'd post messages randomly and relay encrypted sends. Doable, but quite a niche, will leave this for later, once more people are using the system.

- %3Chqm1eynYg1ECCqyAgZLZPHspGpLQQTMiS1a3yW81o=.sha256

## Metadata Privacy

> annomizing the recipient's identity is essential to have decent privacy.
> The thing is the metadata is much easier to analyze than the content. Lets say I send a message "ES6 is a cancer" - any plaintext prose like this has a myriad of interpretations - it doesn't mean I have cancer. If I send a bunch of messages to a doctor who is a cancer expert... uh, probably I wouldn't do that unless I had cancer. To analyze the content, you kinda need a human who can interpret the context. very expensive. But analyzing the metadata graph is very easy. That is why in all the snowden stuff, they hardly analyze the content at all.
>
> The approach you are suggesting is to show the recipient, but allow the recipient to wear a mask. and just change masks rapidly. I'm not ruling out whether this could be made to work - but it would be a lot harder to prove that it works, where as if we encrypt the "to" field we can examin the cryptographic part of the protocol and convince our selves: yup, no way to tell who the recipient is.
>
> regards the replay attack: it would actually be pretty simple to prevent. we just have to introduce something so that a message does not decrypt correctly in a different context. currently, a private-box message has a nonce at the start which is used in all the encryptions in that message. If I copied that whole message it would be the same, but if it worked a different way: instead of using the random nonce - use a hmac of hmac(author + previous, random_nonce) then that the same content copied into another message would now not decrypt. no surprising replays.

- %lgiAaiHPnz+/+B5K7v3nPR/sK/FBlCRb0qiIuvr6ims=.sha256
