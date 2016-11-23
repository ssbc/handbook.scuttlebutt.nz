# Using Trust in Open Networks

Open networks are systems that allow participation without deferring to central authority.
The Web, Email, BitTorrent, IPFS, and SecureScuttlebutt are all open networks.

Open networks try to maximise their potential value by letting agents contribute and extract data independently, and without intermediation.
This is the Laissez-faire approach to architecture, and it frequently benefits from the efficiency of [horizontal scaling](https://en.wikipedia.org/wiki/Scalability#HORIZONTAL-SCALING).

In SecureScuttlebutt, we have decided [never to adopt centralized authorities in the protocol](design-challenge-avoid-centralization-and-singletons.md).
This decision was motivated by
 1. distrust of information monocultures
 2. desire to maximize autonomy of individual users
 3. general curiosity

This constraint pushes us to find novel solutions for shared datastructures.
This article will summarize literature on trust-based mechanisms, and offer some perspective to how they can be applied to SecureScuttlebutt.

---

**Trust-ranking is a key feature of open networks with shared data-structures.**
As each agent receives new information, it must decide how to act on it, and decide whether to discard the input.
Spam, resource-leaching, and DoS attacks would otherwise overwhelm the agents.

Email is an open network: anybody can create a server and account.
And, the inbox a shared structure: users share append-rights over each others' inboxes.
But, without proper spam-filtering, email is nearly useless.
Filtering must be both effective (very little spam) and accurate (*very* few false positives) or email loses its utility.

[A survey of trust in computer science and the Semantic Web](http://www.inf.ufsc.br/~gauthier/EGC6006/material/Aula%206/A%20survey%20of%20trust%20in%20computer%20science%20and%20the%20Semantic%20Web.pdf) names two primary means of managing trust.

> **Policy-based trust**. Using policies to establish trust, focused on managing and exchanging credentials and enforcing access policies. Work in policy-based trust generally assumes that trust is established simply by obtaining a sufficient amount of credentials.

> **Reputation-based trust.** Using reputation to establish trust, where past interactions or performance for an entity are combined to assess its future behavior. Research in reputation-based trust uses the history of an entity's actions/behavior to compute trust, and may use referral-based trust (information from others) in the absence of (or in addition to) first-hand knowledge.

SecureScuttlebutt uses social "following" relations as a base trust-policy.
Users choose which feeds to follow, and therefore opt into every messaging partner.
This is how SSB controls spam.

Other trust-policies could be leveraged by SSB applications, to give users authority over other shared data-structures.
For instance, users could assign friends the right to follow more users on their behalf, or give moderator powers to enable post-hiding.

**However, policies scale poorly, as they require the user to make a decision about every other agent in the network.**
This makes it hard for a user to evaluate information produced by "strangers", even if the stranger is only one or two social hops away.
**To solve this, reputation-based trust can be introduced to build upon the user's decisions, by analyzing the decisions of other agents, and assigning authority *automatically*.**

---

To understand reputation-based trust, let's look at a common application of them, search engines.
PageRank is still one of the top search algorithms in use, so it's important to understand where it fits in the current landscape of research.

[Propagation Models for Trust and Distrust in Social Networks](http://www2.informatik.uni-freiburg.de/~cziegler/papers/ISF-05-CR.pdf) does a good job explaining PageRank's qualities, in section 2.
From there, and from other papers:

 - PageRank is a probabilistic analysis, of a random surfer clicking links through the Web. The common alternative is path-analysis, which is the sort of thing that PGP does in its WoT.
  - [Trust Management for the Semantic Web](https://homes.cs.washington.edu/~pedrod/papers/iswc03.pdf) and [The EigenTrust Algorithm for Reputation Management in P2P Networks](http://ilpubs.stanford.edu:8090/562/1/2002-56.pdf) are two good papers on probabilistic analysis. Both of these try to generalize PageRank. Eigentrust is cited a lot by other papers.
  - [Propagation Models for Trust and Distrust in Social Networks](http://www2.informatik.uni-freiburg.de/~cziegler/papers/ISF-05-CR.pdf) is a good resource for path-analysis, as it explains Advogadro and a novel algorithm called Appleseed.
 - PageRank operates with global information, and seeks to be objective (everyone's opinion) instead of subjective (google's opinion). Google crawls the Web to get global knowledge of the graph.
 - PageRank infers that links are recommendations from one page to another. That's usually a correct assumption, but not always. Semantic Web research tries to use richer signals (explicit recommendations of pages, ratings of trust between agents, ratings of belief in facts, etc) and then construct better analysis. 
 - PageRank relies on weblinks being transitive recommendations. The algorithm does *not* apply for recommendations that aren't transitive. For instance, inter-agent trust signals are not always transitive, and distrust signals are *never* transitive.
 - Because PageRank creates global ratings for pages, it's actually estimating the global *reputation* of a page. Reputation is different from trust, because trust is subjective (from a particular node's perspective) and reputation is objective (from the whole network's perspective).
 - Many algorithms, including Eigentrust and Advogato, rely on a seed set of trusted peers. The seed-set makes it possible to detect malicious rings that work together to elevate their rating. The original PageRank paper doesn't have any such seed-set, but in practice I imagine Google has an equivalent. (I question whether the analysis can be called "objective" if there is such a seed-set.)

These lessons can easily apply when writing graph-analysis algorithms for SecureScuttlebutt.
Inferring the wrong properties about the input data, such as edge-transitivity, can lead the algorithm to draw wrong conclusions.
As the purpose of reputation is to *automate trust decisions*, it's important not to make those mistakes.

The data model is also very important to reputation-based trust, and is frequently explored in the literature I found.
There is no consensus on which model is best; they vary by application and intent.

[The EigenTrust Algorithm for Reputation Management in P2P Networks](http://ilpubs.stanford.edu:8090/562/1/2002-56.pdf) applies probabilistic analysis on a dataset of rated transactions.
After every file-download, users publish whether the downloaded file was as-advertised.
The ratings are accumulated and normalized to quantify the trustworthiness of peers.
The authors assume that trusted peers are likely to make good trust decisions as well, and so they use the trust-values transitively to fill holes in the dataset.
At a glance, [the XRep algorithm](http://eris.prakinf.tu-ilmenau.de/res/papers/security/damiani02reputationbased.pdf) seems to work in roughly the same way.

Eigentrust is not a social system; it's a p2p mesh of file-hosts, which abstracts the hosts away from the user's awareness.
Their data model, therefore, doesn't use direct trust-ratings between agents, whereas SSB can.
In contrast, [the TrustMail algorithm](https://www.cs.umd.edu/~golbeck/pubs/Golbeck,%20Hendler%20-%202004%20-%20Accuracy%20of%20Metrics%20for%20Inferring%20Trust%20and%20Reputation.pdf) sets ratings directly on agents.

[Trust Management for the Semantic Web](https://homes.cs.washington.edu/~pedrod/papers/iswc03.pdf) splits the model into "belief ratings for statements" and "trust ratings for agents"

> [We] propose a solution to the problem of establishing the degree of belief in a statement that is explicitly asserted by one or more sources on the Semantic Web. ... Our basic model is that a user's belief in a statement should be a function of her trust in the sources providing it.

They offer both path-algebra and probabilistic interpretations for the graph, and a number of options for the formulas.

[Modeling and Evaluating Trust Network Inference](http://ebiquity.umbc.edu/_file_directory_/papers/93.pdf) describes an even more sophisticated model.
First, they isolate trust into domains, following the intuition that an agent may be an expert in one field, but not in another.
Then, in section 2.4.2, they define 2 categories of trust, and subdivide them into 5 types.
The categories are *referral trust* ("reflects an agent's estimation about the quality of the other agents' knowledge") and *associative trust* ("reflects the similarity between two agents").
The subdivisions are as follows:
 - Domain Expert Trust (DET) is referral trust that evaluates the quality of an agent's domain knowledge. Intuitively, DET is not transitive, but DET may imply RET (see next item) on the same domain.
 - Recommendation Expert Trust (RET) is referral trust that evaluates an agent's trust knowledge. In real world, the domain used in RET is often much wider than DET, e.g. CNN is a domain expert only in news area, while Google.com is a recommendation expert in almost any area. Moreover, RET in transitive according to its definition, so it can be used to propagate both DET and RET.
 - Similar belief trust (SBT) is an associative trust that evaluates the similarity of two agents' domain knowledge. Intuitively, SBT clusters information providers, and it can be used to propagate DET.
 - Similar trusting trust (STT) is an associative trust that evaluates the similarity of two agents' trust knowledge. Intuitively, STT clusters trustors (agents who maintain trust knowledge), and it can be used to propagate both DET and RET. Computing STT needs trust knowledge from only two agents.
 - Similar cited trust (SCT) is an associative trust that evaluates the similarity of how two agents are trusted.  Intuitively, STT clusters trustees (agents who are trusted) by their reputation, and it can be used to propagate both DET and RET. Reliable SCT requires trust knowledge from a large population of agents.

This is not the first group to separate DET and RET.
The [Hilltop](https://en.wikipedia.org/wiki/Hilltop_algorithm) and [HITS](https://en.wikipedia.org/wiki/HITS_algorithm) algorithms make that distinction as well.

The values used to rate agents or data varies between the algorithms.
Roughly, they tend to be trinary (trusted/distrusted/no-opinion) or real (0..1, or 0..10, etc).
I've found nothing definitive about which is best.

When choosing the model, we should remember that reputation systems exist to rank information in the absense of local input.
If the user were able to rate all inputs a-priori, a policy system would suffice.
Since the user can not, a reputation system merges the inputs of many users to fill holes in the data structure.

If we want to entrust function-critical decisions to shared data, we need to be robust to malicious behaviors.
The [Appleseed Paper](http://www2.informatik.uni-freiburg.de/~cziegler/papers/ISF-05-CR.pdf) provides useful analysis of this:

> The "bottleneck property" [is] common feature of attack-resistant trust metrics. Informally, this property states that the "trust quantity accorded to an edge `s -> t` is not significantly affected by changes to the successors of t."

Put another way, the bottleneck property holds if a voting ring is not able to elevate its reputation the network by recommending each other.
This property requires subjectivity: trust must flow outward from a seed set.
Fortunately, SecureScuttlebutt is subjective by nature.

The other concern we must address is compromise-risk: we should minimize the danger of a trusted node acting maliciously.
Two techniques for handling this:
 - Always distribute authority. A security-critical change should be backed by multiple trusted agents.
 - Watch for anomolous events and alert the user. If a kind of change is rare, confirm it before accepting it.

---

A few notes on how computation occurs.
In addition to the path-algebra vs probabilistic analysis, there's a split among the papers between making distributed vs centralized/localized computations.

Distributed computation uses realtime queries to peers for trust information.
Centralized/localized computation aggregates information at a node, and then computes across that aggregated information.

Both Google and SecureScuttlebutt qualify as centralized/localized.
The difference is that Google tries to obtain global knowledge of the network, via crawling, while SSB obtains a localized neighborhood of the network.

The community is encouraged to supplement SecureScuttlebutt's localized computation with distributed protocols, but it's not currently expected that SSB core will include any distributed computation systems itsemf, due to the scope creep that would create.

---

It may be possible to generalize a universal system for ranking the trust and quality of data in SecureScuttlebutt.
If so, then a single "ranking" application would be able to publish and review data structures.
However, I'm unsure that's possible.
In the near-term, I suggest we study applications and data-structures separately, and watch for unifying principles.

There are a few applications which I think we should focus our attention on, because they'll yield the most insight, and value, to the network.
 - An intelligent crawler which expands on the user's follow relationships. This application would start with the user's explicit follows, and then analyze the network to find feeds, messages, and blobs that are worth downloading. This might be viewed as attempting to automate virality. The algorithm will need to balance its options against available disk space.
 - A search engine for messages, feeds, and blobs. This is a very broad application, and so may be hard to address early, but it will have a lot of relevance, insight, and value for the network. It also makes a strong companion to the intelligent crawler, as it lets you discover what the crawler has fetched for you. And, the queries may act as inputs to the crawler, since queries signal your interests.
 - A whois application. Without name authorities, naming becomes a kind of search that must produce only one result. Challenging, but possibly rewarding.

-Paul F
0Looking
