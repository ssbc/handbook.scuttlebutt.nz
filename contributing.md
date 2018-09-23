# Contributing

![Hermies watering](assets/garden/hermies-watering.gif)

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

The easiest way to start hosting a [Pub server](concepts/pub.md) is to use

- [`ssb-pub`](https://github.com/ahdinosaur/ssb-pub) ([one click installer!](http://butt.nz/install?url=https://github.com/ahdinosaur/ssb-pub)),
- [`easy-ssb-pub`](https://github.com/staltz/easy-ssb-pub),
- or, follow the ["Create a Pub" guide at scuttlebot.io](http://scuttlebot.io/docs/config/create-a-pub.html)

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

## Making a Good Pull Request

Goal: be as easy (for the maintainer) to merge as possible. (This means it can get merged faster.)

### Explain what you are trying to do

All pull requests should have a description explaining what their goal is. Stating a goal helps the maintainer evaluate whether the proposed change is the simplest way to achieve that goal. If the PR is just code then it is much harder to figure out the original intention of that code.

### Document what sort of change it is (patch, feature, breaking change)

What type of change you are proposing affects what you need to communicate.

The main types of changes are:
1. Patches
2. Features
3. Breaking changes

### Patches 
Bug fixing. Documenting this is easy. Explain the problem you intend to fix, and ideally also add a test case that reproduces the problem you found.

### Features
Adding new features is more challenging. Now your PR needs to explain the use-case. Consider the following when writing your PR:
- Why do you want this feature? 
- What problem are you trying to solve with it? 

When you make a pull request you are not just making a change to the code, you are also making a request to the maintainer: you are asking that they acknowledge this change and give this use their blessing. 

When possible, new modules are better than a PR, and then you can ask the maintainer to link to your module's README from their README.

Code style is considered but not usually a deal breaker for a PR, since code style change always change later. However, the API style is very important because breaking changes require changes throughout dependent modules.

For some really popular modules that a lot of code depends on, new features will require a very significant justification of why they are needed.

### Breaking Changes
Breaking changes are rare. However, if you must make a breaking change, one that restricts the API to a more minmal set is most likely to get merged. Expect a proposed breaking change to get lots of discussion.

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
