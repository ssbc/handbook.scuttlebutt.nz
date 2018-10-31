# How can I preserve my privacy when using Secure Scuttlebutt?

## Don't use your real name

Scuttlebutt does not require to use your real name. You can use
whatever you like. If you want to stay a bit more private, choose a name that 
people wouldn't normally associate with you. This is known as a [handle](https://en.wikipedia.org/wiki/User_(computing)).

## Use private messages

[Private messages]((https://www.scuttlebutt.nz/concepts/private-message.html) in Scuttlebutt always use [end to end encryption](https://en.wikipedia.org/wiki/End-to-end_encryption). Although a private messages is relayed throughout your network, they are only readable by the recipients of the message. Other peers can only see that you have sent a private message and not the content of the message or who it has been sent to.

## Only share what you are comfortable with sharing

Most social networks give the illusion of being able to delete your data. In reality once you have published something onto the internet, it is probably going to be there forever in some form or another. Even if you delete the data, someone else may have made a copy of it. 

In Scuttlebutt everything you post can be considered public. Everything you do on SSB is signed with your [secret key](https://ssbc.github.io/scuttlebutt-protocol-guide/#keys-and-identities) which can be used to verify that a post came from the owner of that key (assuming no one else has access to your device). Metadata like who you are communicating with and when you are communicating are also visible to your network. Private messages are the only exception as described above and are only visible to the recipients of that message.

Because Scuttlebutt is a decentralised append only database shared amongst your network, when something is posted it is not possible to delete or edit that content as it has already been propagated to your peers. A Scuttlebutt client such as [Patchwork](https://github.com/ssbc/patchwork) tries to make this clear when you go to post something with a notice stating that "This message will be public and cannot be edited or deleted". Likewise in a private message sent using Patchwork you will see a notice that says something like "Only visible to you and one person that has been mentioned".

## Take responsibility for your communities moderation

The concept of privacy in Scuttlebutt is that you create a trusted network of peers moderated in a human way by your friends. If there is a bad actor in your network, you must rely on yourself and your friends to block that entity and therefore remove them from your network. Scuttlebutt is a network that supports both the practice of [free speech and of free listening](https://www.scuttlebutt.nz/principles/). You and your peers have the tools to create a community of respect and consent without relying on any third parties.

## Keep it in the Scuttleverse

Scuttlebutt has a way of indicating to public gateways (places that mirror Scuttlebutt
content onto the old web such as the volunteer run [viewer.scuttlebutt.io](https://viewer.scuttlebot.io)) that you don't want anything you say to show up there. This opt-out is enabled by default when installing Scuttlebutt using the [Patchwork](https://github.com/ssbc/patchwork) client.

To do this globally for all client, open up your Terminal app and type the following (with `<YOURID>`
replaced with your actual ID).

```
sbot publish --type about --about "<YOURID>" --no-publicWebHosting
```

If you ever want to re-enable it you can say

```
sbot publish --type about --about "<YOURID>" --publicWebHosting
```

## Use Tor to obscure your location
Connecting in a peer to peer manner to exchange gossip messages will reveal your [IP adddress](https://en.wikipedia.org/wiki/IP_address) to other peers which could be be used to de-anonymise you. Luckily, Scuttlebutt has built in support for
the [Tor](https://torproject.org/) which is an anonymity network. See the [SSB handbook page on Tor](tor.md) for more details.

## Use a VPN to obscure your location
You can also use a Virtual Private Network to obscure your [IP adddress](https://en.wikipedia.org/wiki/IP_address). Note that this is not as good for preserving your privacy as using Tor. You have to place a lot of trust in your VPN provider to keep your data safe and a good VPN will also tend to cost you money. Here is some more info on [choosing a VPN that is right for you](https://ssd.eff.org/en/module/choosing-vpn-thats-right-you).

## Use a passphrase and full disk encryption to secure your local device
Part of the security model for Scuttlebutt is that your [secret key](https://ssbc.github.io/scuttlebutt-protocol-guide/#keys-and-identities) is kept safe from unauthorised access. Your secret key is stored unencrypted on your devices file system. For example, under the Linux operating system your secret key can be found at `~/.ssb/secret`. If someone gains access to that file then can impersonate you and access all your data.

You can secure this key by requiring a strong passphrase to unlock your device though it is possible to bypass the passphrase by accessing the storage directly. You can also further secure your data by encrypting the file system of your device. This is referred to as full disk encryption as is available on most popular operating systems. It means your data cannot be accessed when the device is powered off. You can find more information on [keeping your data safe here](https://ssd.eff.org/en/module/keeping-your-data-safe).
