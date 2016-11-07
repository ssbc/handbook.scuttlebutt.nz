# Link

> what I recall is @substack suggested "cypherlink" as the term for a hash used as a link (also called a merkle link in ipfs) which I liked because it sounded like a riff on "hyperlink" and "cypherpunk". After that, "cypherspace" was pretty obvious.
>
> I was staying with @substack and @johnny at the time. The design I had planned was [cyphernet](https://gist.github.com/dominictarr/5990143) but switched to the secure-scuttlebutt design because it was simpler and had more predictable replication performance.

- %mMd+625YFJXxmtDDghUBiVR4jUIqHT+ynlFakBHSWlQ=.sha256

Messages can reference three types of Secure Scuttlebutt entities: messages, feeds, and blobs (i.e. files). Messages and blobs are referred to by their hashes, but a feed is referred to by its signing public key.

To indicate the type of ID, a "sigil" is prepended to the string. They are:

- `@` for feeds
- `%` for messages
- `&` for blobs

Additionally, each ID has a "tag" appended to indicate the hash or key algorithm. Some example IDs:

- A feed: `@LA9HYf5rnUJFHHTklKXLLRyrEytayjbFZRo76Aj/qKs=.ed25519`
- A message: `%MPB9vxHO0pvi2ve2wh6Do05ZrV7P6ZjUQ+IEYnzLfTs=.sha256`
- A blob: `&Pe5kTo/V/w4MToasp1IuyMrMcCkQwDOdyzbyD5fy4ac=.sha256`

When IDs are found in the messages, they may be treated as links, with the keyname acting as a "relation" type. An example of this:

```shell
sbot publish --type post \
  --root "%MPB9vxHO0pvi2ve2wh6Do05ZrV7P6ZjUQ+IEYnzLfTs=.sha256" \
  --branch "%kRi8MzGDWw2iKNmZak5STshtzJ1D8G/sAj8pa4bVXLI=.sha256" \
  --text "this is a reply!"
```

```javascript
sbot.publish({
  type: "post",
  root: "%MPB9vxHO0pvi2ve2wh6Do05ZrV7P6ZjUQ+IEYnzLfTs=.sha256",
  branch: "%kRi8MzGDWw2iKNmZak5STshtzJ1D8G/sAj8pa4bVXLI=.sha256",
  text: "this is a reply!"
})
```

In this example, the root and branch keys are the relations. SSB automatically builds an index based on these links, to allow queries such as "all messages with a root link to this message."
