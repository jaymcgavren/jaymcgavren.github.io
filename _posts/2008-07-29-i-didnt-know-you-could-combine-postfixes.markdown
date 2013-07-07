---
layout: post
title: I didn't know you could combine postfixes...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '882'
  original_post_id: '1005'
  _wp_old_slug: '1005'
---
<pre>
irb(main):009:0&gt; 1 if true unless false
=&gt; 1
irb(main):010:0&gt; 1 if true unless true
=&gt; nil
irb(main):011:0&gt; 1 if false unless false
=&gt; nil
irb(main):012:0&gt; 1 if false unless true
=&gt; nil
</pre>
