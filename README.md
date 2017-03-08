# ssb handbook ![Hermes the hermit crab](assets/hermes.png)

A work-in-progress guide to the ssb-verse and key concepts and influences

## What Is Scuttlebutt?

Historically, sea-slang for gossip - a scuttlebutt is basically a watercooler on a ship.

Scuttlebutt is a decent(ralised) secure gossip platform.

> This seems like a silly name, but I assure you, this is real science. Read this: http://www.cs.cornell.edu/home/rvr/papers/flowgossip.pdf
>
> Or, if you're lazy: http://en.wikipedia.org/wiki/Scuttlebutt (laziness will get you nowhere, btw)

## How To Get Started

The easiest to get started is [patchwork-next](https://github.com/mmckegg/patchwork-next), a classic social networking [application](./applications.md).

![screenshot of patchwork-next](./assets/patchwork-next.jpg)

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

## From NPM

NPM hosts the stable release.
It will be the least likely to have bugs.

**Dependencies:**

 - node v5.3.x (you might like to use [nvm](https://github.com/creationix/nvm))
 - npm v3.5.x ([Instructions to update NPM when using NVM](#updating-npm))

**Install:**

``` bash
npm install ssb-patchwork -g
```

**Run:**

```bash
patchwork
```

Then open `localhost:7777`.


## From Git

GitHub hosts the development version.
It will contain updates not yet published on NPM.

**Dependencies:**

 - node v5.3.x (you might like to use [nvm](https://github.com/creationix/nvm))
 - npm v3.5.x ([Instructions to update NPM when using NVM](#updating-npm))

**Install:**

```bash
git clone https://github.com/ssbc/patchwork.git
cd patchwork
npm install
```

**Run:**

From directory you cloned patchwork to:

```bash
npm start
```

Then open `localhost:7777`.

**Update:**

From directory you cloned patchwork to:

```bash
git pull origin master
npm install
```

```

```

patchwork is a discussion platform that we use to anything and everything concerning ssb and decentralization.
patchbay is another take on patchwork - it's compatible, less polished, but more modular. The main goal of patchbay is to be very easy to add features to.
git-ssb is git (& github!) on top of secure-scuttlebutt. Although we still keep our repos on github, primary development is via git-ssb.
it is recommended to get started with patchwork, and then look into git-ssb and patchbay.

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

Scuttlebutt is not the only project working in a decentralised space. Here are a few other projects also working on solutions:

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
