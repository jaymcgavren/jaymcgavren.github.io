---
layout: post
title: iTunes-style folder organization...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '758'
  original_post_id: '829'
  _wp_old_slug: '829'
---
Hrmmm, not bad:

<pre>
irb(main):001:0&gt;
Utility.cache(
	'foo',
	:creator =&gt; 'Jay McGavren',
	:title =&gt; 'Cache Test',
	:sort_order =&gt; 1,
	:parent_directory =&gt; '.',
	:extension =&gt; 'txt',
	:album =&gt; 'My Album'
)
=&gt; nil
irb(main):002:0&gt; puts find "Jay McGavren"
Jay McGavren
Jay McGavren/My Album
Jay McGavren/My Album/01 Cache Test.txt
=&gt; nil
irb(main):003:0&gt; puts cat "Jay McGavren/My Album/01 Cache Test.txt"
foo
</pre>

[edited for legibility]
