# Identity

Your identity is "who you are".

## True Name

In Scuttlebutt, your [True Name](http://dominictarr.com/post/106497926352/asymmetric-cryptography-works-like-magic) is represented as an [ed25519 key pair](http://ed25519.cr.yp.to/) using [libsodium](https://github.com/jedisct1/libsodium) ([why?](http://dominictarr.com/post/133109715357/which-js-crypto-library-should-i-use)).

The private key is your secret not to be shared with anyone. The public key is used as your identifier.

There is no worldwide store of identities. Users must exchange pubkeys, either by publishing them on their feeds, or out-of-band.

> There is no session, and no logon. your identity is represented by a private key that is stored in on your computer.
>
> In ordinary websites, the server is the guardian of your identity,
> and grants it to you. This is the reverse, you are your own guardian.
>
> When you make a post, it creates a signed record, that appends to a history of things you have done. When my computer sees your messages,
>
> it knows it's, well, actually it doesn't know who you are, but it knows you are the same identity as before.

- %ox29TwlaATzXebEwpmzenTQKD2XN2cBrihCsHNm6qKE=.sha256

> So in the future, how i figure it will work, is when a child is born, the parents generate a private key for it. The parents could easily know the private key... and maybe that is for the best. But later, when the child is mature enough to understand the consequences, they would generate their own private key. Now they are cryptographically an adult.

- %9M3KSMrxigeIxJDIdVgm9HmBL7dg71eHMVnGYwDbByI=.sha256

> oh, sorry, let me clarify one thing I said wrong.
>
> There are two types of asymmetric cryptography (not actually the whole story but will do for now) signing, and exchange.
>
> you create a signature with a signing (private) key, and it's verified with a corresponding public key.
>
> Then there are also exchange keys, or called diffie-helman keys. There isn't really a widely used name for this type of key, mainly i think because it doesn't have a simple real-world metaphor like "signing" does. Anyway, exchange keys take _your_ public key, and _my_ secret key then combines the together to produces a shared exchange key.
>
> In `nacl` this operation is called `scalarmult`. That is an implementation detail really, in classic DiffieHelman a different mathematical operation is used, but it has the same behavior. That is, we can each take the other's public key, and our own secret key, and produce a key that essentially represents a relationship between us.
>
> In nacl both types of keys are used, signing keys are ed25519 keys, and exchange keys are curve25519 keys. `sign` uses `ed25519` keys, and `scalarmult` takes `curve25519`.
`box` takes two exchange keys, and then uses `scalarmult` internally. There is also another function `secretbox` that just takes a symmetric key, say the output of `scalarmult`.
>
> To encrypt a private key, you probably don't encrypt it _to_ anyone, so `secretbox` is the one to use. Also, you'll need to generate the key the first time, and then later, you'll need to restore it. To do that, you need a _seed_. That is just a random number, but make sure it's _really_ random. instead of encrypting the private key, encrypt the seed, then regenerate the keypair from that seed.

- %lBglUeQhHbKRGigcXXZmeQOTXisoSAI9J3X6vnxsDhA=.sha256

## Nick Names

In Scuttlebutt, anyone can set a nickname (petname) for another peer. It's akin to a human-memorable symlink to a cryptographic identifier.

> The web you are familiar with is organized like a property system. If you can claim a username, you "own" it. not here. here, you name is whatever people call you.
> You can suggest a name, and an avatar, and we can use it. and you can rename us. This may seem unfamiliar at this point in history, but it is the natural way of the world.

- %1H99noUzO+kUrj8zwX0stfuUvX29X8HgXjHErfnwkOY=.sha256

> In a centralized system, the database is the source of all truth and enforcer of rules. Enforcing a rule like "all names must be unique!" is easy.
>
> In a decentralized system, like ssb, there is no single source of truth. peers must enforce a rule with collective action. This makes for a _lot_ more wiggle room. To put it in database terms, it means anyone can write anything, but other clients will ignore what they think is invalid.
>
> So, names is patchwork are somewhat like IRC, except that when I mention you @akkartik it records both your human name and your public key, then I sign this message, so there is a cryptographic record that I call `@1DfC2qFuXuli/HOg3kJbKwxiOpc3jXLdJD3TnhtzWNs=.ed25519` "akkartik"
>
> I can call you anything. Unlike IRC, but like "real life", other people choose your name. So, in ssb, a _name_ is just a mapping from a string to a cryptographic token (i.e. public key, and git-ssb repos also have names)
>
> If I start using a new name for you, my old messages will still bear the name I used then, but it would still link to your public key.

- %7hcvpITRduLDNKpLqN6Xm+8d/t7aQu2YqZhBO3CtSC0=.sha256

> Don't ask anyone's _opinion_ on a name, that is just a bikeshed, get people to use it and see what they _call_ it. Let names emerge, like winning at charades.

- %am/DGQpKliHYgsYgUUXk4UHwz9rgn+0WN4oc4yq97Mw=.sha256

> @amnovak just because you can name it anything doesn't mean that it will be total chaos.
> No one enforces natural language, we can invent new words that "arn't in the dictionary", but since people want to be understood, that is enough consistency.

- %nrZecbFGe/Vx7tSUAfZMWM2/wZKnC7CdyTyvo6R7mxI=.sha256

> petnames should be a user aid: you can enter the url as a petname, and then the computer gives you back the exact name, which you can share securely. we loose a lot more than we gain with a naming registry. like, the recent npm thing. names become "property" instead of granted by the community.

- %oJtA0Lmj7PBo9KmkC99/cVHhNzi9+ulXAwvJvMIJY60=.sha256

> Yes! Anyway, all naming is subjective!
> It's just that sometimes one opinion is privledged above others.

- %9s3P86A9UoiMpsGg/ffiIs0zl6YpDXvAl3MW7vP39t0=.sha256

## Trust

> Implicit vs. Explicit: we can interpret something like twitter or fb or the web as a "reputation network", but most people don't actually think about that while they use it. So, just create an _implicit_ reputation network, people just use it because it works for them, you don't need to pitch them on "reputation network".
>
> For example, google traverses the links on all the websites they find, analyzes that graph and uses them to determine a _ranking_ for all websites. That ranking score can be interpreted as "reputation". The authors of those web links may not be thinking "here is a reputable site" or "I want to increase this website's score" but you can interpret this as an expression of trust, not because of the link but more because of the sites _they choose not to link to_. Linking is an _action_ that expresses trust (involves a risk), not just a statement "I trust X", which is pretty cheap.
>
> Another really interesting thing about page rank, is the graph represents a mathematical model of how humans "surf" the internet. refresher: before search engines where any good, you'd just click around from links to links, go to some site, follow it's links, etc. pagerank simulated this, calculating the probability that if you'd land on a given page if you spent your life just randomly clicking on links. I think the key here is that pagerank is based on a model of what _humans already do_, it just makes it faster.
>
> Gameability - how easy is it to create the appearance of trust/value?
systems like ebay have "feedback" which seems easy, and works in the case of ebay because ebay charges a transaction fee which would make it expensive to create a fake reputation. For example: I could create a bunch of ebay accounts and make my sock puppet accounts "buy" from me, then give me good feedback, so it would appear I made many transactions. However, even though I don't post the goods (to myself) I'd still have to pay the ebay transaction fee! So if you see someone on ebay who has made thousands of transactions, the transaction fees for those may add up to more than they could make if they ripped me off one one transaction, so I can be pretty confidant in making that purchase.
>
> In a decentralized system like ssb, an identity is just a key pair, and I could generate thousands of those a second, it would be really easy to create sock puppets that appeared to "trust" me. Any realistic reputation system would need to have a way to rule this out - a straight sum of all the feedback probably wouldn't work, but something that traced a social graph might.

- %1S7PrZmAAC3foX/aAIO0wRoaFnVG9xL3YMvnKwba4xQ=.sha256

> "trust" and "reputation" have no formal definition, and everyone "already knows" what they mean. sillicon valley has coopted the term "reputation" where it's something they calculate from their mass of data. in a human context, "reputation" is obviously subjective, although, to some degree an estimation of a collective sense of trust. In an honour-amoungst-theves sense, one community can esteeme someone highly, doesn't mean another community sees it like that. I have been meaning to try and write a glossary of ways people use the term "trust" and "reputation" because there are too many senses to agree on a definition. That WoT thing was just frustrating, for me, because everyone had a valid view, that was completely different.

- %Dwd9MKS1uD+yM1MeiiYLgYrTujtkrWoKHhV9bZzeQn0=.sha256

## Groups

> To summarize, our ideas are that a group, by definition has an inside and an outside, and they also may have internal behaviour and external behaviour. Internal behaviour means it's possible to communicate privately with other members, external behaviour means it's possible for the group to speak/act as one. I want it to be possible to follow a group like you would follow an individual, ideally without needing the ssb to treat it differently (that depends on the right crypto though)
>
> this thread has a [good summary of our group ideas](%HRmMuXxv+4SzJkXVs+oy5K3PnEEi1kP8NOkID7auywc=.sha256)

- %b8/CYP0xj+fXgB2u5eDOQUbBCqyJ+sXv/CvuZNDOVVA=.sha256
