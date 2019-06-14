# How much space will scuttlebutt take up on my computer?

---

This depends on how long you've been on scuttlebutt, how many friends you have, and how many high-quality kitten pics you send each other.

Since you are holding the entire, evergrowing log of your friend network, it could grow rather large over time.  The biggest storage space would be in your blobs folder, since that is holding all the attachments(kitten pics) sent to one another.   

For a better example of size, we can look at two users' .ssb folders: @keks and @cryptix.

Here is @keks folder:

	2.5G  ~/.ssb/blobs
	7.5K  ~/.ssb/blobs_push
	512 ~/.ssb/config
	125M  ~/.ssb/db
	272M  ~/.ssb/fulltext0
	512 ~/.ssb/gossip.json
	20M ~/.ssb/links
	1.5K  ~/.ssb/manifest.json
	122M  ~/.ssb/media
	60M ~/.ssb/node_modules
	7.9M  ~/.ssb/query
	1.0K  ~/.ssb/secret`

And here is @cryptix's:

	32K   ./blobs_push
	9.5M  ./query
	28M   ./links
	172M  ./node_modules
	195M  ./db
	317M  ./fulltext0
	1.2G  ./blobs
	1.9G .

In both cases, blobs take up significant space.  If this is a concern, you can delete the blobs folder.  Patchwork will fetch any blobs needed the next time you log on--assuming they still live in the folders of your friends.  If you are the last person to have held onto the blob with the image of a cat falling asleep inside a cereal box, and then you delete that blob folder...that image is gone from the scuttleverse.  All you have now are the memories (though let's be honest, you've probably saved that picture somewhere else cos it sounds incredible.)

---

**Sources**
* Answer compiled from these threads:

- %bUEQtn85jtL8Vxjup4sS/7wcaswS4fThUPVH7G5IvjU=.sha256
- %Ayi7UUbJnIZ12S/gbHof60oHBlmjdrv7TUyFCq5cOTQ=.sha256

Shoutouts to @cryptix and @keks for awesome answers.
