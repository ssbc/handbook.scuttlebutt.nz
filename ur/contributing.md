# Contributing

This project is open commons that anyone can improve.

We welcome all contributions, such as but not limited to:

- code
  - bug reporting
  - features
  - tests
  - peer review
  - protocol design
- operations
  - pub server hosting
- design
  - project artwork
  - user testing
  - newbie first impressions
  - real-world use cases
- storytelling
  - blogs
  - talks
  - documentation
- facilitation
  - community organizing (meetups)
  - group collaboration
  - conflict resolution

If you contribute enough, you'll be invited to join the [project members](https://github.com/ssbc).

We aim for autonomous solving of collaborative problems with a common vision.

## Hosting a [Pub server](concepts/pub.md)

The easiest way to start hosting a [Pub server](concepts/pub.md) is to use [`easy-ssb-pub`](https://github.com/staltz/easy-ssb-pub).

Or, follow the ["Create a Pub" guide at scuttlebot.io](http://scuttlebot.io/docs/config/create-a-pub.html).

## Contributing Code

To understand what code is in the Scuttlebutt ecosystem and how the modules assemble together, see [the "Modules" page](modules.md).

To get started developing [Patchwork](https://github.com/ssbc/patchwork) (the primary user interface), first [follow the instructions to build from source](https://github.com/ssbc/patchwork/blob/master/README.md#or-build-from-source).

To get started developing [Scuttlebot](https://github.com/ssbc/scuttlebot) (the data server), see the ["Introduction to Using Scuttlebot" guide](https://ssbc.github.io/docs/scuttlebot/tutorial.html).

### Native Build Dependencies

The main build dependecies are `libsodium` and `leveldb`.

They should be automatically built using a C++ compiler on `npm install` as we use [chloride](https://github.com/dominictarr/chloride) and [level](https://github.com/Level/level), respectively.

### Tests

If contributing to a low-level module, please include tests.

### Code Style

The default recommended code style is [standard](https://standardjs.com/).

If existing code is in another style, [please respect the code style](https://groups.google.com/forum/#!msg/nodejs/MWaivVTirPY/0pnRjKsggkIJ). :)

### Licenses

Most code is licensed under a permissive license (MIT / ISC), while other code like Patchwork is licensed under a copyleft license (GPL / AGPL).

## Contributing Documentation

While over time we have scattered documentation around:

- [scuttlebot.io](https://scuttlebot.io)
- [ssbc.github.io](https://ssbc.github.io)

Our intention is to combine these sources and have this handbook ([`ssb-handbook`](https://github.com/ssbc/ssb-handbook)) be the new location for all documentation relating to Scuttlebutt.

You can clone, build, and serve this handbook with `gitbook` locally.

The `SUMMARY.md` is the manifest on which the compiled gitbook is based. Edit that if you want content in/out of the book.

### Contributing With `git-ssb`

To use the public portal for the handbook code, browse to <https://git.scuttlebot.io/%25lJsDWwnF4bDxHWYuSjw%2FbW37xg%2BsaF8WtPZYZsefKj0%3D.sha256>.

To use your local scuttlebot server to clone the handbook code:

```bash
npm install git-ssb -g
git clone ssb://%lJsDWwnF4bDxHWYuSjw/bW37xg+saF8WtPZYZsefKj0=.sha256 ssb-handbook

cd ssb-handbook
npm install
npm start
```

To contribute to the handbook code, make a pull request with

```
git ssb pull-request
```

### Contributing with GitHub

Our public GitHub repository is at [ssbc/ssb-handbook](https://github.com/ssbc/ssb-handbook)

Feel free to make an issue or pull request here if you see something that needs doing.
