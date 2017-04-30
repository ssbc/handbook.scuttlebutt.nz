# Where does all my data live?

---

It lives on your computer, your friends computers, and your friends' friends computers.

 When you connect to a friend over an application like Patchwork, you are syncing the diaries that live on your computers, and making sure they hold the same relevant information. This helps explain how no internet connection is needed: as long as there is _any_ way for your two computers to talk to each other, you can catch up on each other's feed.

 On your computer, your diary lives as a hidden directory within your home directory. You can find it by opening up your terminal and, from the home directory, typing in `ls -a`. The scuttlebutt directory is called `.ssb.`

The messages you've sent live in a leveldb database within this folder (specifically at `.ssb/db`.  They are stored in binary form and so are pure gibberish if you try to read them directly from that folder.     

**Additional Resources**

- If the command line and terminals are new to you, here is a great in-depth introduction:
[Taming the Terminal](https://www.bartbusschots.ie/s/blog/taming-the-terminal/)

**Sources**
* Answer compiled mostly from experience and [this thread.](https://viewer.scuttlebot.io/%25bUEQtn85jtL8Vxjup4sS%2F7wcaswS4fThUPVH7G5IvjU%3D.sha256)  Shoutouts to @cryptix for the answer on encryption and the leveldb database.
