# Install Scuttlebot

## From NPM

NPM hosts the stable release.
It will be the least likely to have bugs.

**Dependencies:**

 - node v4 and greater (you might like to use [nvm](https://github.com/creationix/nvm))
 - node-gyp (```npm install -g node-gyp```)
 
***Linux Dependencies***
Installation may fail when building the libsodium dependencies due to missing aclocal. On Ubuntu you will need to run:
 
```bash
sudo apt-get install autotools-dev automake
```

**Install:**

```bash
npm install ssb-server -g
```

**Run:**

Start scuttlebutt server.

```bash
ssb-server start
```

Then, in another session, use the cli tool to access the API:

```bash
ssb-server whoami
ssb-server publish --type post --text "Hello, world"
ssb-server log
```

You can get help with `-h`.


## From Git

GitHub hosts the development version.
It will contain updates not yet published on NPM.

**Dependencies:**

 - node v4 and greater (you might like to use [nvm](https://github.com/creationix/nvm))
 - node-gyp (```npm install -g node-gyp```)
 
***Linux Dependencies***
Installation may fail when building the libsodium dependencies due to missing aclocal. On Ubuntu you will need to run:
 
```bash
sudo apt-get install autotools-dev automake
```

**Install:**

```bash
git clone https://github.com/ssbc/ssb-server.git
cd scuttlebot
npm install
```

**Run:**

From directory you cloned scuttlebot to:

```bash
./bin.js server
```

Then, in another session, use the cli tool to access the API:

```bash
./bin.js whoami
./bin.js publish --type post --text "Hello, world"
./bin.js log
```

You can get help with `-h`.

**Update:**

From directory you cloned scuttlebot to:

```bash
git pull origin master
npm install
```
