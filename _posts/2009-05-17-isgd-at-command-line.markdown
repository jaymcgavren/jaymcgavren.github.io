---
layout: post
title: is.gd at command line...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1017'
  _oembed_c65fbb5565fb612b072284e371fc5099: '{{unknown}}'
  original_post_id: '1209'
  _wp_old_slug: '1209'
---
Saved this on my PATH as shrink_url...

<pre>
#!/bin/sh
curl "http://is.gd/api.php?longurl=$(echo $@ | sed 's/ /+/g')"
</pre>

Which lets me do this:

<pre>
$ shrink_url http://current.com/items/90029658_death-star-destroys-enterprise.htm
http://is.gd/xHYe
</pre>

Pipe to clipboard and you're ready to paste into a browser.  I suppose I could also enclose the result in a $() call to my favorite command line Twitter client, but I'm not feeling that fancy yet.

<pre>
$ shrink_url http://current.com/items/90029658_death-star-destroys-enterprise.htm | cb
$ cb
http://is.gd/xHYe
</pre>
