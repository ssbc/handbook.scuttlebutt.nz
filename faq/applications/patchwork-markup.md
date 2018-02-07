# Is there a list of possible markdown for Patchwork?

*Patchwork messages can be written with markdown, but what specific flavor or dialect of markdown?  I want a style guide!*

---
Here you go!

	***
	Emphasis, aka italics, with *asterisks* or _underscores_.

	Strong emphasis, aka bold, with **asterisks** or __underscores__.

	Combined emphasis with **asterisks and _underscores_**.

	Strikethrough uses two tildes. ~~Scratch this.~~

	1. First ordered list item
	2. Another item
	  * Unordered sub-list. 
	1. Actual numbers don't matter, just that it's a number
	   1. Ordered sub-list
	4. And another item.  

	   Some text that should be aligned with the above item.

	* Unordered list can use asterisks
	- Or minuses
	+ Or pluses

	[I'm an inline-style link](https://www.google.com)

	[I'm a reference-style link][Arbitrary case-insensitive reference text]

	[You can use numbers for reference-style link definitions][1]

	Or leave it empty and use the [link text itself]

	URLs and URLs in angle brackets will automatically get turned into links. 
	http://www.example.com or <http://www.example.com> and sometimes 
	example.com (but not on Github, for example).

	Some text to show that the reference links can follow later.

	arbitrary case-insensitive reference text]: https://www.mozilla.org
	[1]: http://slashdot.org
	[link text itself]: http://www.reddit.com
	
	Quotes
	> Quotes are done as blockquotes.
	This line is part of the same quote because there is nothing to break them up

	This line has an empty line above it so will appear as unquoted

	> And then this one will be a new block quote
	
The above yields:

Emphasis, aka italics, with *asterisks* or _underscores_.

Strong emphasis, aka bold, with **asterisks** or __underscores__.

Combined emphasis with **asterisks and _underscores_**.

Strikethrough uses two tildes. ~~Scratch this.~~

1. First ordered list item
2. Another item
  * Unordered sub-list. 
1. Actual numbers don't matter, just that it's a number
   1. Ordered sub-list
4. And another item.  

   Some text that should be aligned with the above item.

* Unordered list can use asterisks
- Or minuses
+ Or pluses

[I'm an inline-style link](https://www.google.com)

[I'm a reference-style link][Arbitrary case-insensitive reference text]

[You can use numbers for reference-style link definitions][1]

Or leave it empty and use the [link text itself]

URLs and URLs in angle brackets will automatically get turned into links. 
http://www.example.com or <http://www.example.com> and sometimes 
example.com (but not on Github, for example).

Some text to show that the reference links can follow later.

[arbitrary case-insensitive reference text]: https://www.mozilla.org
[1]: http://slashdot.org
[link text itself]: http://www.reddit.com

Quotes
> Quotes are done as blockquotes.
This line is part of the same quote because there is nothing to break them up

This line has an empty line above it so will appear as unquoted

> And then this one will be a new block quote


---
*Sources*

This answer was taken almost verbatim from @nanomonkey's fantastic answer on Patchwork.
