# What happens if I delete or lose everything?

*What happens if I unfollow all my friends and delete my .ssb folder? Will all my messages disappear from the scuttleverse?*

---

Your feed would be deleted off of your computer, but would remain on your friends'(and friends of friends) computers. Your messages would remain as long as your friends remained connected, but they might be harder to find in the future as the network grows.

If you wish to recover your account, you would have to have at least one file: `~/.ssb/secret` and then you could sync with a friend (for instance through a common LAN) to redownload all of your feed data. It is easier to recover your account if you also backup the file `~/.ssb/gossip.json`, but it is not absolutely necessary, like `~/.ssb/secret` is. In the future – with a project called [Dark Crystal](https://darkcrystal.pw/) – we want to easily enable you to backup your `~/.ssb/secret` with your friends, so that even if you lose all your data, your friends are enough to recover your account.

But if you just want delete your account on purpose, your friends may still temporarily have your messages stored. In this, again, it is similar to real-life social relationships. If you decide one day to ditch all your friends and move away... it doesn't mean these friends will forget about you. And they may still talk about that one time you screamsang Carly Rae Jepsen at karaoke.  But as life continues, and you all make new friends and connections and live new stories, that specific memory may become harder to recall.

## Deleting and 'resetting' your .ssb database

If things get 'corrupted' locally and you want to resync your .ssb data from your peers you could do the following to create a clean copy,  

These instructions assume you are using terminal on OSX or Linux but, the same steps should also run on Windows.

First **back up your .ssb dir** which is probably in your home directory, `~/.ssb`
```
> cd ~                                          
> mkdir ssb_bak                                                                   
> cp -rp .ssb ssb_bak
```

_If you get this error on the last step, you can safely ignore it:_
```                                                               
cp: .ssb/socket: Operation not supported on socket
```

Next **copy your secret file and gossip.json** back 
```
rm -rf .ssb
mkdir .ssb
cp ssb_bak/.ssb/secret .ssb
cp ssb_bak/.ssb/gossip.json .ssb
```

You can now **resync from your peers** by starting your preferred ssb server

If you are using ssb-server (previously sbot) you can do this as follows. 
```
ssb-server start
```

It will take a while to resync everything so give it a while. It's imporant to wait until your feed completely syncs before posting (or linking) anything, or you can fork your feed. Once your `~/.ssb` dir is restored you can safely restart patchwork or other programs which will read from the same dir.

---

**Sources**
* Answer compiled from these threads:

- %9tfp/8bCful8ZvMskklXYO6C/7/gIaBKH9jNwJI6+TM=.sha256
- %AyrmGv9lfW6cFb2DVUGjUW//OdaEo3bRGELZkgZGmWs=.sha256

Shoutouts to @claytonkoenig for asking the question, and to @ezdiy, @keks and others for their answers.
