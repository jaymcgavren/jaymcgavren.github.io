---
layout: post
title: Naughty, but I like it...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '841'
  original_post_id: '939'
  _wp_old_slug: '939'
---
Normally you can't add objects to an array like this:

<pre>
irb(main):001:0&gt; [1] + 1
TypeError: can't convert Fixnum into Array
        from (irb):1:in `+'
        from (irb):1
</pre>

But Array#+ tries to call to_ary() on its target if it's not already an array.  So just add that method, and voila:

<pre>
irb(main):002:0&gt; class Fixnum; def to_ary; [self]; end; end
=&gt; nil
irb(main):003:0&gt; [1] + 1
=&gt; [1, 1]
</pre>

Wait, why stop there?

<pre>
irb(main):005:0&gt; class Object; def to_ary; [self]; end; end
=&gt; nil
irb(main):007:0&gt; [1] + "foobar" + File.new('test.xml')
=&gt; [1, "foobar", #&lt;File:test.xml&gt;]
</pre>

Of course, you should probably be using Array#&lt;&lt; for this.  But I wonder what other applications there are...
