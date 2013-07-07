---
layout: post
title: Extlib for everyday use...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '981'
  original_post_id: '1148'
  _wp_old_slug: '1148'
---
Looks like a couple of my core enhancements may be reinventing the Extlib wheel, so...

<pre>
irb(main):002:0> "foo\nbar".compress_lines
NoMethodError: compress_lines not defined
  from /Users/jay/ruby/lib/utility/enhancements.rb:12:in `method_missing'
  from (irb):2
irb(main):003:0> exit
</pre>

FAIL.  A tweak to DeferredActiveSupport (now DeferredExtensions)...

<pre>
-module DeferredActiveSupport
+module DeferredExtensions
   def method_missing(method, *arguments, &block)
     require 'activesupport'
+    require 'extlib'

 class String

-   include DeferredActiveSupport
+   include DeferredExtensions

#And other classes...
</pre>

And retry:

<pre>
jay@dandelion:~
$ /Users/jay/Shortcuts/ruby\ shell
irb(main):001:0> "foo\nbar".compress_lines
=> "foo bar"
</pre>

Yay!  I don't even know everything I've gained yet.  Time to play around a bit.
