# Publish Encrypted Messages

You can publish messages which are encrypted for up to 7 other recipients.
This is done with the `private` plugin.

## Private.publish

First is [private.publish](../api/scuttlebot-private.md):

```js
sbot.private.publish({ type: type, ... }, recps, cb)
```

This works exactly like `sbot.publish`, but `recps` includes a list of feed-ids to encrypted the message for.
(Note, the CLI is currently not able to support this function, so it must be called programmatically.)

## Private.unbox

To decode a message, you use [private.unbox](../api/scuttlebot-private.md)

```js
sbot.private.unbox(ciphertext, cb)
```

An encrypted message's `content` attribute will be a string.
So, you can see that a message is encrypted with this check:

```js
function isEncrypted (msg) {
  return (typeof msg.value.content == 'string')
}
```

## Private Posts

There is no way to see who an encrypted message is for.
If `unbox()` decrypts successfully, then you'll know the message was for you.

A private post should include the `recps` attribute, so that the recipients know who else received the message.
Example usage:

```js
sbot.private.publish(
  {
    type: 'post', 
    text: 'secret hello!',
    recps: [
      { link: '@hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519', name: 'paul' },
      { link: '@EMovhfIrFk4NihAKnRNhrfRaqIhBv1Wj8pTxJNgvCCY=.ed25519', name: 'dominic' }
    ]
  },
  [
    '@hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519',
    '@EMovhfIrFk4NihAKnRNhrfRaqIhBv1Wj8pTxJNgvCCY=.ed25519'
  ],
  cb
)
```

Be sure to include yourself amongst the recipients and encryption targets, or you won't be able to read your own message!