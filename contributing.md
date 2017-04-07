# Contributing

## [Scuttlebutt](https://scuttlebutt.nz) (project)

TODO

## [Patchwork](https://github.com/ssbc/patchwork) (user interface)

TODO

## [Scuttlebot](https://github.com/ssbc/scuttlebot) (server api)

TODO

## [ssb](https://github.com/ssbc/secure-scuttlebutt) (data protocol)

TODO

## Handbook (documentation)

You can clone, build, and serve this with gitbook locally.

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
