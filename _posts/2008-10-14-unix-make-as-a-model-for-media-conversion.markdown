---
layout: post
title: 'Unix “make” as a model for media conversion...'
tags: []
status: publish
type: post
published: true
meta:
  original_post_id: '1081'
  _wp_old_slug: '1081'
---
OK, this is a lot less complicated than I thought.  From <a href="http://frank.mtsu.edu/~csdept/FacilitiesAndResources/make.htm">An Introduction to the UNIX Make Utility</a>:

<blockquote>

Make has a set of default rules called suffix or implicit rules. These are generalized rules that make can use to build a program. For example in building a C++ program these rules tell make that .o object files are made from .cc source files. The suffix rule that make uses for a C++ program is

<pre>
     .cc.o:
        $(CXX) $(CXXFLAGS) -c $&lt;
</pre>

where $&lt; is a special macro which in this case stands for a .cc file that is used to produce a particular target .o file.

</blockquote>

So in the media server, if I mark my compiler object as requiring type binary/o, and link a text/cc to it, the compiler object should look at the environment for rules that output binary/o.  Among them, it will (hopefully) see one linked to a compiler object that takes text/cc.  (I know in the real world these compilers are the same, but this is my contrived example and I'm sticking to it.)  It feeds the text/cc into the compiler linked from the rule, then feeds the binary/o output to the initial target compiler.

OK, let's try a better example: we have a Screen which expects a binary/image, and we link a text/html to it.  We go find a rule that links to ImageMagic "convert", which outputs a binary/image, but only accepts text/plain input.  Looking for rules that output text/plain, we find one linked to "lynx" that accepts text/html.  So the path goes:

<pre>text/html -&gt; text/plain -&gt; binary/image</pre>

This could probably be drawn out to several more steps, though I worry about speed in finding the correct path.  If I recall right, looking up "graph traversal" in Programming Game AI By Example will help me there.
