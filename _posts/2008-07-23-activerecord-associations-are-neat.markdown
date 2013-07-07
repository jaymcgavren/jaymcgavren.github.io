---
layout: post
title: ActiveRecord associations are neat!
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '891'
  original_post_id: '1000'
  _wp_old_slug: '1000'
---
{% highlight ruby %}
class Album < ActiveRecord::Base
	has_many :songs
end
{% endhighlight %}

<pre>
&gt;&gt; album.songs &lt; [#]
&gt;&gt; album
=&gt; #
&gt;&gt; song
=&gt; #
</pre>

Note that empty album_id...

<pre>
&gt;&gt; album.save
=&gt; true
&gt;&gt; song
=&gt; #
</pre>

album_id is populated...

<pre>
mysql&gt; select * from songs;
+----+----------+-------------+--------------+
| id | album_id | name        | track_number |
+----+----------+-------------+--------------+
|  1 |        8 | First Track |            1 |
+----+----------+-------------+--------------+
</pre>

And the song is saved as well.  Nice to have stuff done for me for once!  (Let's see if my attitude changes when Rails volunteers to do something I didn't want done.)
