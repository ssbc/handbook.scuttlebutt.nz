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

## Groups

> To summarize, our ideas are that a group, by definition has an inside and an outside, and they also may have internal behaviour and external behaviour. Internal behaviour means it's possible to communicate privately with other members, external behaviour means it's possible for the group to speak/act as one. I want it to be possible to follow a group like you would follow an individual, ideally without needing the ssb to treat it differently (that depends on the right crypto though)
>
> this thread has a [good summary of our group ideas](%HRmMuXxv+4SzJkXVs+oy5K3PnEEi1kP8NOkID7auywc=.sha256)

- %b8/CYP0xj+fXgB2u5eDOQUbBCqyJ+sXv/CvuZNDOVVA=.sha256
