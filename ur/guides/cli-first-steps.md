# First steps with sbot, a command line tool for Scuttlebutt

I'm new to Scuttlebutt and Patchwork, and writing this as I start to explore its possibilities with the sbot command line tool. Feel free to respond with any suggestions or questions. My interest in Scuttlebutt was piqued by [@andrestaltz](@QlCTpvY7p9ty2yOFrv1WU1AE88aoQc4Y7wYal7PFc+w=.ed25519)'s post, [An Off-Grid Social Network](https://staltz.com/an-off-grid-social-network.html), especially how the decentralized, peer-to-peer architecture works to support offline use and avoids reliance on any servers with special authority.

Scuttlebutt applications depend on a *server* component that maintains the connection with the Scuttlebutt network. Many Scuttlebutt applications, including Patchwork, use [Scuttlebot](https://github.com/ssbc/scuttlebot) in this role as a server, and interact with the Scuttlebutt network via Scuttlebot. The first time you run Scuttlebot (or an application using it), an identity is created (in the form of a public and private key pair) and this identity is used by all applications that communicate via Scuttlebot.

**sbot** is a command line tool included with Scuttlebot. To install it, install the *scuttlebot* Node.js package globally by running:

```
npm install --global scuttlebot
```

This should let you run *sbot* on the command line. Let's start by using **whoami** to verify that sbot can connect to a Scuttlebot server and has the right identity.

If you are connected to the Scuttlebutt network, this command should return a user ID. For example, this shows running *sbot whoami* and it returning my user ID:

```
$ sbot whoami
{
  "id": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519"
}
```

If you are not connected to the network, you will see an error message like this:

```
$ sbot whoami
Error: Could not connect to the scuttlebot server.
Use the "server" command to start it.
```

To connect to the network, you can either start Patchwork or another application that uses Scuttlebot, or run *sbot server*, which starts the server component.

On the Scuttlebutt network, each user has a *feed* or *log* made up of messages signed by the user. Only the user can write to their feed, since only the user should possess the identity's private key and be able to sign messages with it. Users interact with each other by publishing messages on their own feed that mention users, establish a *follow* link with another user, or link to the message of another user.

Let's use the **latestSequence** command to find how many items are in my feed. For example, this shows running *sbot latestSequence* with one argument (my user ID) and it returning the last sequence number in my feed and the timestamp of this item:

```
$ sbot latestSequence "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519"
{
  "sequence": 24,
  "ts": 1491624622201
}
```

Using JavaScript, I can convert this timestamp into a localized date to verify that this was the date and time of my last message:

```
$ echo "console.log(new Date(1491624622201).toLocaleString());" | node
4/7/2017, 11:10:22 PM
```

Next, let's use the **createUserStream** command to retrieve items from my feed. This command has many options, including a mode to perform a full retrieval of the feed and a *live* mode where messages appear in real-time as they arrive.

With the *limit* argument, we can retrieve the first item from my feed. For example:

```
$ sbot createUserStream --id "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519" --limit 1
{
  "key": "%S/nfXzDK3waYEaEDwwGA7FsIqFzpIiU3200Lf0aG/Ps=.sha256",
  "value": {
    "previous": null,
    "author": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
    "sequence": 1,
    "timestamp": 1491533348827,
    "hash": "sha256",
    "content": {
      "type": "about",
      "about": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
      "name": "arithmetric"
    },
    "signature": "B/I1k24ihHsivqzo+G01M/rqQWCIC8YYlt7+EiKoovdd1C36b8/RU+DgFO80lzNNPWWakgh9K+vY2hdslelMAQ==.sig.ed25519"
  }
}
```

Notice that the *sequence* value is 1 and the *previous* value is null. Also, this is an *about* type message made with Patchwork that identifies my user ID with the name *arithmetric*.

By adding the *reverse* argument to the *sbot createUserStream* command, we can retrieve the last item from my feed. For example:

```
$ sbot createUserStream --id "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519" --limit 1 --reverse
{
  "key": "%hl3+i0yaWRo2DG11VdpQhXx/ol2lbf73W9rdHbiaV5c=.sha256",
  "value": {
    "previous": "%rQ6UTukySj3b3igS0M4FTBB/H/VmM3U8Z6gwtp3v4iY=.sha256",
    "author": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
    "sequence": 24,
    "timestamp": 1491624622198,
    "hash": "sha256",
    "content": {
      "type": "contact",
      "contact": "@FbGoHeEcePDG3Evemrc+hm+S77cXKf8BRQgkYinJggg=.ed25519",
      "following": true
    },
    "signature": "p8ekEHID8uqomyXyPUssHtjrGGKxJleU4waqHm9mPwA6WHLu4jAIG0+uoLPsJ/LkXUAMK1Jub9qC33ib6btpCQ==.sig.ed25519"
  }
}
```

This message has a *sequence* value of 24, which matches the last sequence number from the *latestSequence* command above. This message is the *contact* type with *following* set to true, so it is the message recording my action to follow the user in the *contact* field.

Now, let's use the **get** command to get the message previous to the last one. The *sbot get* command accepts one argument, the message ID. For example, this shows running get with the message ID in the previous field above and the message response:

```
$ sbot get "%rQ6UTukySj3b3igS0M4FTBB/H/VmM3U8Z6gwtp3v4iY=.sha256"
{
  "previous": "%jhaGHJiDINuSp1gr6nHbxhB9BCW9HIPtGR3ntdN3EWM=.sha256",
  "author": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
  "sequence": 23,
  "timestamp": 1491611316858,
  "hash": "sha256",
  "content": "cZOlfY2YQBMqIKkX7zKwnlZ8eC2gElbmk2HOoXGW/tkYberzSW3k3rw1XJxuJKavmSHNCF9e4hWVCueIFa2ibFOxxkuEy13rYk1YGmWj4xgxx1Vv4hUuLIsdeRM50XH+7OTkAejkc2pu+4NYXZDbmuINX8djUrddjwq3VDUbk...",
  "signature": "gYceZ6gv7Kd2L78uCYsEwro/q8Y+BNSyeNoSshtIbfN4T6ZZ3bz5JyU8qt/q4ecNSaSjj1pxaGM+UQ9NOsdQDQ==.sig.ed25519"
}
```

Notice that the content value is not a JSON object. This is an example of an encrypted private message. Since this private message is in my feed, I can decrypt it with the **private.unbox** command. For example, this shows running this command with the encrypted value and receiving the decrypted JSON message content:

```
$ sbot private.unbox "cZOlfY2YQBM..."
{
  "type": "post",
  "text": "hello world! this is a test encrypted message",
  "mentions": [],
  "recps": [
    "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519"
  ]
}
```

That's just a brief introduction to the Scuttlebutt network using the sbot command line tool. For more information, check out the [API/CLI reference](https://ssbc.github.io/scuttlebot/api.html) and the [Secure Scuttlebutt](https://ssbc.github.io/secure-scuttlebutt/) protocol overview.
