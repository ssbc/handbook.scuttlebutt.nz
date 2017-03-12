# ssb handbook ![Hermes the hermit crab](assets/hermes.png)

A work-in-progress guide to the ssb-verse and key concepts and influences

## What Is Scuttlebutt?

Historically, sea-slang for gossip - a scuttlebutt is basically a watercooler on a ship.

Scuttlebutt is a decent(ralised) secure gossip platform.

> This seems like a silly name, but I assure you, this is real science. Read this: http://www.cs.cornell.edu/home/rvr/papers/flowgossip.pdf
>
> Or, if you're lazy: http://en.wikipedia.org/wiki/Scuttlebutt (laziness will get you nowhere, btw)

## How To Get Started

The easiest way to get started is using [patchwork-next](https://github.com/mmckegg/patchwork-next), a classic social networking [application](./applications.md).

![screenshot of patchwork-next](./assets/patchwork-next.jpg)

## Download and Install Patchwork

On macOS, download the latest .dmg file from [patchwork-next/releases](https://github.com/mmckegg/patchwork-next/releases)

On other operating systems, with [node and npm installed](https://github.com/creationix/nvm):

```shell
$ git clone https://github.com/mmckegg/patchwork-next
$ cd patchwork-next
$ npm install
$ npm start
```

On Linux you'll need some more dependencies for the spell-checker. On Debian/Ubuntu:

```sh
sudo apt-get install libxext-dev libxtst-dev libxkbfile-dev
```

### Be Invited To A Pub

In order to gossip outside your local network, you'll need to connect to a [Pub](./concepts/pub.md).

Here's an 100-use invite to @mixmix's pub:

```txt
pub.mixmix.io:8008:@uRECWB4KIeKoNMis2UYWyB2aQPvWmS3OePQvBj2zClg=.ed25519~gq+n8AXMdhzwnGWZxWitgczTkbr70drnbEaOi3Noo5M=
```

In `patchwork-next`, click "+ Join Pub" and paste the code.

This will cause you to follow @mixmix's Pub and vise versa. If you haven't synchronized to this social network yet, prepare to wait a few minutes while your local server synchronizes.

## About This Handbook

To view the public gitbook, browse to <http://scuttlebutt.nz>.

You can also build and serve this with gitbook locally. The following assumes you're running a scuttlebot server and are in the follow neighbourhood of mixmix or his pub.

```bash
npm install git-ssb -g
git clone ssb://%lJsDWwnF4bDxHWYuSjw/bW37xg+saF8WtPZYZsefKj0=.sha256 ssb-handbook

cd ssb-handbook
npm install
npm start
```

The `SUMMARY.md` is the manifest on which the compiled gitbook is based. Edit that if you want content in/out of the book.

> If you see a job that needs doing - that is your job.

## Other Projects

Scuttlebutt is not the only project working in a decentralized space. Here are a few other projects also working on solutions:

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
