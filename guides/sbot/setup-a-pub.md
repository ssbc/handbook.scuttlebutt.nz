# Setup a Pub

Note, this guide assumes moderate technical ability.

## 1. Get the Server

Pub servers need a static, publicly-reachable IP address.
The easiest way to get a public server is by renting a virtual server from businesses such as [Amazon](https://aws.amazon.com/), [Linode](https://www.linode.com/), or [Digital Ocean](https://www.digitalocean.com/).

After renting the server, follow the guides provided by your host to configure the software.
We recommend using a common Linux distribution, such as Ubuntu.

Scuttlebot by default uses port `8008`, so make sure to expose that port (or whatever port you configure scuttlebot to use) to the internet.

## 2. Install Node

On the server, install [NVM](https://github.com/creationix/nvm):

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.1/install.sh | bash
```

Then install node 5.3.x:

```bash
nvm install 5.3
nvm alias default v5.3.0
```

And update NPM to 3.5.x:

```bash
npm install -g npm@3.5
```

## 3. Install Scuttlebot

Install Scuttlebot using NPM.
(If you prefer to install using git, [follow the instructions here](./install.md)).

```bash
npm install -g scuttlebot
```

To update scuttlebot in the future, simply run the global install again.

## 4. Create a run-sbot.sh script

Save the following script somewhere easy to find, such as `~/run-sbot.sh`.
This script will help ensure uptime, even if scuttlebot experiences a crash:

```bash
#!/bin/bash
while true; do
  sbot server --host {your-hostname}
done
```

Be sure to replace `{your-hostname}` with the actual hostname of your server
For instance, if your server is `foobar.com`, then you should enter `sbot server --host foobar.com`.

## 5. Run the server script

Use a session-manager such as [screen](https://www.rackaid.com/blog/linux-screen-tutorial-and-how-to/) or [tmux](https://wiki.archlinux.org/index.php/Tmux) to create a detachable session.
Start the session and run the script:

```bash
sh ~/run-sbot.sh
```

Then, detach the session.

## 6. Confirm Scuttlebot server is running

To check if sbot is running, use the following command:

```bash
sbot whoami
```

If all is well, your Pub's ID will be logged to the console.
If this fails, check that the server-script is still active, and isn't failing during startup.

## 7. Create the Pub's profile

It's a good idea to give your Pub a name, by publishing one on its feed.
To do this, first get the Pub's ID, with `sbot whoami`.
Then, publish a name with the following command:

```bash
sbot publish --type about --about {pub-id} --name {name}
```

It's a good idea to use your Pub's hostname.
Also, don't use spaces, or include the `@` symbol.
Here's an example usage (dont copy this!):

```bash
sbot publish --type about --about @2mIg4e/GO53+hKJBBrn+KZtb+1aMYazb/9FGEHoQp3U=.ed25519 --name foobar.com
```

## 8. Create invites

For a last step, you should create invite codes, which you can send to other users to let them join the pub.
The command to create an invite code is:

```bash
sbot invite.create 1
```

This may now be given out to friends, to command your pub to follow them.
If you want to let a single code be used more than once, you can provide a number larger than 1.

## 9. Backup your data directory (optional)

It's a good idea to regularly backup the Pub's data directory, in case of failures.
The data-directory will include the Pub's keypair, messages, and files.
It can be found at `~/.ssb`, where `~` points to the home directory of the user running Scuttlebot.
