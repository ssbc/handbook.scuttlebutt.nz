# Publish a Post

Publishing messages in Scuttlebot is very simple:

```bash
ssb-server publish --type {type} [...attributes]
```
```js
sbot.publish({ type: type, ... }, cb)
```

The "post" type is a generic text-based message.
Here's an example publish command:

```bash
ssb-server publish --type post --text "hello, world"
```
```js
sbot.publish({ type: 'post', text: 'hello, world' }, cb)
```

## Schema

The full schema of a post message is:

```js
{
  type: 'post',
  text: String,
  channel: optional String,
  root: optional MsgLink,
  branch: optional MsgLink,
  recps: optional FeedLinks,
  mentions: optional Links
}
```

## Posting to a Channel

To post to a channel, just include the name of the channel, without the #.
For instance, to publish to '#patchwork-dev':

```bash
ssb-server publish --type post --text "hello, world" --channel patchwork-dev
```
```js
sbot.publish({ type: 'post', text: 'hello, world', channel: 'patchwork-dev' }, cb)
```

## Posting a Reply

Replies use the `root` and `branch` attributes of posts.
The `root` should give the ID of the topmost post in the thread, whereas `branch` has the ID of the immediate parent.
If replying to the topmost post, then `root` and `branch` will be equal.

Here's an example of replying to the topmost post:

```bash
ssb-server publish --type post --text "I agree!" --root %cfts5CAC/KIg1MNCbDXMVXPVhPsc4dRNWMXO2dNrN9Y=.sha256 --branch %cfts5CAC/KIg1MNCbDXMVXPVhPsc4dRNWMXO2dNrN9Y=.sha256
```
```js
sbot.publish({ type: 'post', text: 'I agree!', root: '%cfts5CAC/KIg1MNCbDXMVXPVhPsc4dRNWMXO2dNrN9Y=.sha256', branch: '%cfts5CAC/KIg1MNCbDXMVXPVhPsc4dRNWMXO2dNrN9Y=.sha256' }, cb)
```

If the thread is in a channel, be sure to include the `channel` attribute as well.

## Mentioning a User

The `mentions` attribute lets you explicitly reference other users, messages, or files.
If a link is present in `mentions`, then it's usually because the name of the mentioned object is in the text of the post.

Here's an example of mentioning a user:

```bash
ssb-server publish --type post --text "hello, @paul" --mentions.0.name paul --mentions.0.link @hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519
```
```js
sbot.publish({ type: 'post', text: 'hello, @paul', mentions: [{ name: 'paul', link: '@hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519' }] }, cb)
```

## Setting Recipients

When a post is private, it will be [encrypted](howto-publish-encrypted-messages.md).
Because Scuttlebot's encrypted form doesn't include any metadata about who the message is encrypted to, you'll need to include the recipients list in the `recps` attribute.

Note, you should only use `recps` in encrypted messages.
It's not really meant for public messages.
