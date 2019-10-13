# Use an Invite

If you want to connect to your friends across the net, you need to be followed by a Pub server.

First get an invite-code from a Pub operator you know, or [setup your own pub](howto-setup-a-pub).

If you're using Patchwork, you can use the UI to use the code.
However, if you want to use Scuttlebot, you can use the following command:

```bash
ssb-server invite.accept {code}
```

Your Scuttlebot will now connect to, and sync with, the Pub.
Other users can sync with the pub to receive your log.
