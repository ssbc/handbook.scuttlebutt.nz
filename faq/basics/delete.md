# What happens if I delete or lose everything?

*What happens if I unfollow all my friends and delete my .ssb folder? Will all my messages disappear from the scuttleverse?*

---

Your feed would be deleted off of your computer, but would remain on your friends'(and friends of friends) computers. Your messages would remain as long as your friends remained connected, but they might be harder to find in the future as the network grows.

If you wish to recover your account, you would have to have at least one file: `~/.ssb/secret` and then you could sync with a friend (for instance through a common LAN) to redownload all of your feed data. It is easier to recover your account if you also backup the file `~/.ssb/gossip.json`, but it is not absolutely necessary, like `~/.ssb/secret` is. In the future – with a project called [Dark Crystal](https://darkcrystal.pw/) – we want to easily enable you to backup your `~/.ssb/secret` with your friends, so that even if you lose all your data, your friends are enough to recover your account.

But if you just want delete your account on purpose, your friends may still temporarily have your messages stored. In this, again, it is similar to real-life social relationships. If you decide one day to ditch all your friends and move away... it doesn't mean these friends will forget about you. And they may still talk about that one time you screamsang Carly Rae Jepsen at karaoke.  But as life continues, and you all make new friends and connections and live new stories, that specific memory may become harder to recall.

---
**Sources**
* Answer compiled from [this thread.](https://viewer.scuttlebot.io/%259tfp%2F8bCful8ZvMskklXYO6C%2F7%2FgIaBKH9jNwJI6%2BTM%3D.sha256) Shoutouts to @claytonkoenig for asking the question, and to @ezdiy and @keks for their answers.
