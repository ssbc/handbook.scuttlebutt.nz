# Feed

A feed is a signed append-only sequence of messages. Each identity has exactly one feed.

Note that append-only means you cannot delete an existing message, or change your history. This is enforced by a per-feed blockchain. This is to ensure the entire network converges on the same state.

## Is Scuttlebutt a Blockchain?

> The main difference is that ssb does not use Proof of Work to choose the next valid block for a global blockchain. Instead, each identity gets their own personal blockchain (i will use "sigchain"). So bitcoin is 1 blockchain, ssb is many sigchains.
>
> The following will be true of pretty much any secure decentralized system:
>
> Both use hashes as links to build structures. bitcoin and ssb are both based around chain structures. ssb also use links to create trees (eg, discussion threads)
>
> Both use signatures to represent an actions performed by an identity, and public keys to represent that identity.

- %o7qQdE9/NKbNuy1anZIoOWrnsfFF3Cef7ozZwrNcRdQ=.sha256

> It mainly differs in philosophy. secure-scuttlebutt avoids not just centralization, but also global singletons. So there is no DHT.
> Both are built on the concepts of hashes as links and public keys as identity.
>
> Then the main structure in ssb is that each user's feed is an append-only signed chain. This structure is very simple, and optimized for efficient replication. To get all you latest updates, I just have to tell a mutual friend the latest sequence number I have received from you.
(on ipfs, i'd have to work backwards from your latest ipns value)
I think a forward replicating database is easier to reason about and build other things on top of.
>
> Since there is no global network, everything depends on your social network. That is the gamble here. But, I think it's a good one. Life has confusingly many options - but we have a simple solution, ask your friends. Spam filtration is the same thing from the other end, what do i not want to see. Take things like the search on google play store - it's so fully of crap (and full of spam reviews) that you are better off asking on twitter. I call twitter solicited spam. since it's pull only, it just doesn't have the same spam problems as email (except for mentions/replies/favs)
>
> By default, you replicate the feeds you directly follow, and the feeds they follow. this provides availability for the network, and also means you can see replies from someone you don't directly follow. it creates a soft boundry to your social network, so once we scale, you won't get spam in your mentions, etc.

- %XnwMywLJAWqRXCAt9YmPuIghlr9tyAZNiKgbDOg385g=.sha256

## [Non-repudation](https://en.wikipedia.org/wiki/Non-repudiation)

> With a signature chain, you'd still have that even if it where possible to "forget" parts, because someone probably has that post, and they'd be able to come forward, and everyone could verify that was the deleted post.
> 
> Having peruasive non-repudation also means that you can't claim someone said something they didn't, so you can't post a doctored screenshot because no one will believe it.

- %ZmudAToEvD6baAFDkrUjj28ySXhI7CRGWRvuYLwMmtQ=.sha256

> @johnny that is true. You could abandon your account, throw your hands up and claim "i've been hacked!!!" that might be a bit harder to pull off credibly (depending on exactly what you where trying to delete)
>
> But I have a more radical idea, I'm not sure if the world is ready for it, but here it is: you could apologise. Then the bad post would show back links to the apology, and readers could interpret it in the new context.

- %xwlk7+jk+jTLvaTq/0G8T5YaoXTacM7Gb7Ko8xVUtuY=.sha256

## Consistency

> I hate to rain on a parade, but one thing is that the relationship between boats is a lot more libertarian than the relationship between the crew of one boat. Even Plato uses the example of the ship at sea to argue for his idea of the geek dictator ("philosopher king").
The crew are literally "all in the same boat" and so there isn't really much room for disagreement. Historically, western culture has decided that the best way to run a boat is under the command of a single captian, and not many people have argued with this. I wouldn't be surprised if it's impossible to ensure the boat without a designated captian. I think this will create a tension that you'll have to work around, at least.
>
> On the other hand, if this was a flotilla of boats... then I think you'd begin to see a natural harmony between you idea and decentralization. Islands of consistency in a sea of eventualness.
>
> Prehaps, you could pitch this not as a single vessel, but as a prototype for a flotilla... maybe invite current sea captians to join your network? That way you might be able to release some of the inevitable pressure of forcing participants into too small a space (1 ship)

- %2vsznn20SD82ChXVcMKKt4J2/Cjcle1pjMFI+bpYjkM=.sha256
