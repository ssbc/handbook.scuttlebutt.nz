# Secure private channels: the good, the bad, and the ugly

By: [Dominic](@EMovhfIrFk4NihAKnRNhrfRaqIhBv1Wj8pTxJNgvCCY=.ed25519)

researching what makes a good connection protocol for secure-scuttlebutt, am investigating different protocols to see what level of privacy & simplicity is achievable.

One thing that is fairly obvious is the TLS is not very good, and unsuitable for a p2p protocol.
In a p2p protocol we can usually regard key management as a solved problem - with the web, there is the whole CA system to certify that a given peer (ip address) is actually the owner of the given domain, but in a p2p system peers are identified by their public key (which is stable) and not their ip address, which is unstable. Usually there is a some sort of look-up system to get the ip addresses,  
so it may not be necessary to send the key inside the connection.

## private-stream

[private-stream](https://github.com/dominictarr/private-stream) is a very simple private protocol that I wrote. It provides encryption, but not authentication. That is, you cannot be sure exactly who you are talking to, but you may be sure that no one else is listening. It is a symmetrical protocol, in that client and server handshake are identical. Each peer sends a Diffie Helman public key + an Initialization Vector (8 byte random number). The DH keys are combined to produce a shared key, and a cipher streams (salsa20) are constructed using the shared key and the two ivs so that each channel (A->B, and B->A) have the same key but different IVs (which is sufficient for security)

I was considering putting authentication inside of this protocol but I am now re-evaluating that.

### dramatization of private stream

Alice and Bob meet in a dark alleyway

Alice & Bob (simultaniously) passes each other a secret note, also with random number written on outside.

> Alice and Bob now combine their secret, with the secret they received and the random numbers,
> to communicate with each other.

Alice does not know who Bob is and vice versa, but no one can tell what they are saying either.

### Further Reading

* [readme](https://github.com/dominictarr/private-stream)

## bittorrent obfuscation

BT encryption is not well regarded, but because it chooses insecure algorithms, not because it's abstract design is bad. It provides the same assurances (or it would, if it's ciphers where secure) as private-stream, except it's a little uglier because it's not symmetrical. (the stream has to know whether it's the caller (client) or answerer (server), so it can derive a distinct key)

### Dramatization of Bittorrent Obfuscation

Alice and Bob meet in an alleyway wearing silly costumes.
They do not realize there is a security camera.
Luckily nobody really cares what they are up to.
Alice and Bob exchange notes and feel like they are spies.
etc, etc.

### Further Reading

* [bittorrent creator on why obfuscation is silly](http://bramcohen.livejournal.com/29886.html)
* [message stream encryption](http://wiki.vuze.com/w/Message_Stream_Encryption)
* [wikipedia page](https://en.wikipedia.org/wiki/BitTorrent_protocol_encryption)

## tls

### dramatization of a TLS handshake:

Alice: "hello, I speak english, spanish, and mandarin"
> (alice opens connection, and describes the cihper suite she supports)

Bob: "hi this is bob and I speak english, just ask carl"
> (bob selects cipher, identifies himself, with a reference.
> carl is a respected member of the community (a CA) who knows bob (has issued bob a cert).
> alice may choose to quickly contact carl to check if bob is cool)

Alice:
  (whispers) "hey bob, the key is 'foofoo'"
> (alice chooses a secret and encrypts it to bob)

> Bob/Alice now encrypt all further messages with the key.

### Further Reading

* [tls handshake](http://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_handshake)

## SSH

SSH seems very complicated and has a variety of methods of authenticating. Flexibility in a security protocol is bad because then there are more edge cases and thus more surface area to audit / cracks for bugs to hide in. [djb agrees](http://curvecp.org/security.html)

SSH differs from our model p2p protocol because there is no key/address lookup system, and so a client cannot know that it's information on a host is uptodate. Also, it may only update information about a host by connecting to it

### Dramatization of SSH connection

Alice: "hi I want to talk to you, in english, spanish or mandarin (prefer english)"
> Alice opens a connection, and lists the ciphers she supports, with preference.

Bob: "hi I speak in english, spanish or mandarin (prefer english), okay lets whisper now"

Alice: passes a secret note to Bob
> generates DiffieHelman key, sends public DH key to bob.
> begins DH exchange

Bob: passes a note back, with I AM BOB signed on the outside.
> bob replies with bob's public DH key, bob's public RSA key, and a signature to prove they are bob.
> Alice now knows she is talking to Bob, Bob does not know who Alice is yet,
> but they do have secure communication now.

To be honest, this seems a little unfair on bob. He has answered the phone and identified himself to a stranger. It happens to be his friend Alice, but it _could_ be a telemarketer, who is now updating their database because they now know where bob lives.

Alice and Bob now have secure communication, and inside that, Alice authenticates to Bob.
I think the reason that SSH is designed this way is to support a variety of client authentication protocols, such as password, host based (checks the ip address of the client (!)), keyboard interactive (usually used for a password, the client's keyboard is directly connected to a program running on the server so it can be literally anything (!)), and finally, pubkeys.

We are only interested in pubkey based authentications.

The following is all private so Alice and Bob can speak normally.

Alice: hey I'm alice and I want to use pubkey auth with `algorithm` and `key`

Bob: okay go ahead "Alice"

Alice: see it's me: _signed, Alice!_

Bob: Alice it is you!!!

### Further Reading

* Architecture of SSH protocol [rfc4251](http://tools.ietf.org/html/rfc4251)
* SSH transport protocol [rfc4253](http://tools.ietf.org/html/rfc4253) (encryption, and server auth)
* SSH Client Authentication Protocol [rfc4252](http://tools.ietf.org/html/rfc4252)

## CurveCP

djb's new Mutual Authenticated UDP based protocol. DJB seems to like to solve all the problems at once, so CurveCP fixes tcp as well as tls. CurveCP is unconfigurable, so there are no edge cases around cipher suite negotiation (yay!). Interesting features of the design include making intro packets sent by the client and server the same size, so that attackers cannot goad the server into wasting more resources than they do (neat!). Also, it has forward secrecy. But all these concerns do make it a little complicated.

CurveCP uses Boxing as the only primitive. A box is encrypted to a recipient key, and signed by the sender. I think the signature is inside the box, so that only the recipient can open and verify.

### Dramatization of CurvesCP handshake

Alice generates a temporary identity Andy.

Alice says: "Hi call me Andy" and Boxes a message from Andy (that is all zeros)
> Alice sends her temporary identity (Andy) to Bob.
> And a message of zeros boxed by Andy.
> this is so that her message is not longer than bobs (we'll ignore this for now)

Bob generates a temporary identity Betty.

Bob boxes a message to Andy: "hi call me Betty, also please remember this code word: c00k13z"

> Bob sends his temporary identity to Alices temporary identity.
> Bob does not know who Alice is yet, but he knows that Alice knows who he is,
> (otherwise he would not have been able to decrypt her message!)
> so he boxes it as Bob (note: this means an eavesdropper who knows bob's long term key can confirm this server is bob... but this is likely to be public information anyway?)
> the cookie is actually some secret information that bob wants to use again
> but he sends it to Alice because he is busy and doesn't want to remember it (allocate memory)
> because he is worried about people wasting his time (Denial of Service attacks)

Alice now knows that she is talking to Bob, and that Bob knows she knows this.

Alice boxes Andy's id to Bob, and then Andy boxes _that box_ to Betty, then sends it back, along with the cookie.
> Bob can now unpack Andy's box (as Betty), and then finds a box from Alice inside that is addressed to Bob, containing Andy's key. Now Bob knows he is talking to Alice.

Bob and Alice now know who they are talking to,
(although they will continue to converse as Andy and Betty instead, sneaky!)

From now on, they just box messages as Andy and Betty,
except that Andy includes Andy's pubkey along with the box.

Later they will make up new secret identities and discard Andy and Betty.
Alice and Bob always create new temporary identities whenever they talk to _anybody_.

### Conclusion.

curvecp is good but has a few minor problems.

* A replay attacker may confirm that a server is actually bob (since the first message is boxed, if a server does respond to that packet, then that indicates it managed to decrypt the first packet... a server *could* respond with a correctly sized nonsence packet, but a protocol design that avoids this would be better.
* If Bob's keys are compromised, an attacker can connect to Bob and pretend to be _anyone_ (who's public key you know!). This could again be solved by signature authentication at the application layer, but any cryptomodule should be designed to _avoid all surprising edgecases_. Expecting users to make up for design flaws via interactions between layers in their cryptosystem is inviting disaster!

A protocol that took the best ideas from curvecp but also solved these two problems would be very robust.

### Questions

* why does Alice include Andy's pub key is every message?
  it seems like it is so that Bob doesn't have to remember Andy,
  but he does still need to remember that is who he is talking to...)

* what are the properties of a "box" exactly?
  [answer](https://github.com/ssbc/scuttlebot/wiki/a-secure-secure-channel-(WIP)#crypto_box)

### Further Reading

* [curvecp website](http://curvecp.org)

### ipfs's secure channel

[ipfs](http://ipfs.io) contains a simple secure channel protocol. It encrypts the content of the session with forward secrecy, prevents replay and man-in-the-middle attacks. It does leak some metadata: the keys that are communicating are shared in plaintext, and thus a passive eavesdropper can see who is talking to who. The protocol is symmetrical, so there is no difference between the client and server messages.

### dramatization of ipfs-secure-channel connection

Alice and Bob (simultaniously): Hi, I am {Alice,Bob}. I speak {ciphers,key-exchange,hashes}. {random number}
> Alice and Bob both open with a packet containing their public key, a nonce, and the cipher suite they support.
> Alice and Bob both select the cryptographic functions to use (key-exchange, hash, cipher) by hash(Alice's nonce + Bob's key) and comparing that to hash(Bob's nonce + Alice's key). Although the hash function used by the protocol is negotiated, at this point it uses a hard coded hash (sha256). Also, ipfs encodes hashes as [multihash](https://github.com/jbenet/multihash), which start with an identifier and then a length. These are bytewise compared, and that determines who's cipher suite has preference. (It seems the intention here is to ensure that cipher suite selection is fair. Forcing the ciphersuite could lead to some attacks, such as a downgrade attack. However, it is fairly easy, if Alice knows she is contacting Bob, to mine for a nonce such that hash(Bob's key, nonce) is very high, and thus likely to win the cipher selection)
> (Personally, I feel having a ciphersuit selection process at all is troublesome, and express my thoughts about it in the [original pull request](https://github.com/ipfs/go-ipfs/pull/34))
> Once the order is decided, each peer selects each {KeyExchange, Cipher, Hash} by taking the order winner's first choice which is also supported by the other peer.

Alice and Bob (simultaniously): you said X, and I said Y, and here is my key exchangep. signed, Alice/Bob :lock_with_ink_pen:

> Alice and Bob now send a DiffieHelman key, and a signature. Alice's signature is: `sign(Alice's hello + Bob's hello + Alice's DH key)`. Bob's is `sign(Bob's hello + Alice's hello + Bob's DH key)`.

>When Alice and Bob receive the other's key, they know whether or not they are _really_ talking to Alice/Bob. 
> Since Alice and Bob sign not just their DH key, but also (indirectly) each other's nonces then replay attacks and man-in-the-middle attacks are impossible. An attacker could replay the hello message, but since the exchange packet depends on the other's hello packet, and contains an unpredictable nonce, then a replayed exchange packet will be invalid. Also, _assuming that the client (caller) knew which server (answerer) they intended to contact, and abort the connection if an unexpected peer responds_ then a man-in-the-middle attack is not possible either. A man in the middle could present a new key, appearing to the server to be a different peer, but the client was expecting to contact a specific server, and aborts the channel before sending anything more.

> If Alice and Bob are satisfied they are talking to the correct peer, they initialize the encryption.

Alice and Bob (simultaniously): here is the random number you gave me.

> Alice and Bob both send back the the nonce the other sent to them. This confirms they are authorized with the other peer, and can now begin secure communication. (NOTE: this means that the first nonce.length bytes of the ciphertext are a [high entropy] plaintext known to an eavesdropper) I don't think there is any special reason to send the nonce back, it might as well be the string "ACCESS GRANTED" (unless I am mistaken?)

ipfs-secure-channel is quite simple, although it could be a little simpler I think. It's basic properties are reasonable, although I think it would be better to remove cipher suite selection because that creates a better primitive.
