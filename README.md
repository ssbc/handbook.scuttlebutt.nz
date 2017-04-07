# ssb handbook ![Hermes the hermit crab](assets/hermes.png)

A work-in-progress guide to the ssb-verse and key concepts and influences

## What Is Scuttlebutt?

Historically, sea-slang for gossip - a scuttlebutt is basically a watercooler on a ship.

Scuttlebutt is a decent(ralised) secure gossip platform.

> This seems like a silly name, but I assure you, this is real science. Read this: http://www.cs.cornell.edu/home/rvr/papers/flowgossip.pdf
>
> Or, if you're lazy: http://en.wikipedia.org/wiki/Scuttlebutt (laziness will get you nowhere, btw)

## How To Get Started

The easiest way to get started is using [patchwork](https://github.com/ssbc/patchwork), a classic social networking [application](./applications.md).

![screenshot of patchwork](./assets/patchwork.jpg)

## Download and Install Patchwork

Download installers for Windows, macOS and Linux from [patchwork/releases](https://github.com/ssbc/patchwork/releases)

Or you can build from source with [node and npm installed](https://github.com/creationix/nvm):

```shell
$ git clone https://github.com/ssbc/patchwork
$ cd patchwork
$ npm install
$ npm start
```

On Linux you'll need some more dependencies. On Debian:

```shell
sudo apt-get install libxext-dev libxtst-dev libxkbfile-dev g++ m4 automake libtool
```

### Be Invited To A Pub

In order to gossip outside your local network, you'll need to connect to a [Pub](./concepts/pub.md).

You can find an invite to an available pub at the [Pub servers registry](https://github.com/ssbc/scuttlebot/wiki/Pub-Servers).

Get an invite, then in `patchwork`: click "+ Join Pub" and paste the invite code.

This will cause you to follow the Pub and vise versa. If you haven't synchronized to this social network yet, prepare to wait a few minutes while your local server synchronizes.

## Join The Community

- **#new-people**: introduce yourself
- **#faq**: first impressions, what is confusing as a new user?
- **#patchwork**: report bugs, suggestions, etc
- **#scuttlebutt**: protocol related discussion

## About This Handbook

To view the public handbook, browse to <http://scuttlebutt.nz>.

The handbook is organized by topics:

* [Talks](talks.md)
* [Applications](applications.md)
* [Principles](principles.md)
* [Contributing](contributing.md)
* [Stories](stories/index.md)
* [Modules](modules.md)
* [Concepts](concepts/index.md)
* [Glossary](glossary.md)

## Other Projects

Scuttlebutt is not the only dex project:

- [Matrix](http://matrix.org/)
- [Bitcoin](https://bitcoin.org/)
- [Ethereum](https://www.ethereum.org/)
- [Zerocoin](http://zerocoin.org/)
- [MaidSafe](http://maidsafe.net/)
- [IPFS](https://ipfs.io/)
- [Dat](http://datproject.org/)
- [Solid](https://github.com/solid/solid)
- [cjdns](https://github.com/cjdelisle/cjdns)
- [Syncthing](https://syncthing.net/)
- [Indie](https://ind.ie/)
- [Twister](http://twister.net.co/)
- [WebTorrent](https://webtorrent.io/)
- [StrongLink](https://github.com/btrask/stronglink)
- [RetroShare](http://retroshare.sourceforge.net)
- [ZeroNet](http://zeronet.io)
