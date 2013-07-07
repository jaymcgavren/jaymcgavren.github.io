---
layout: post
title: 'RubyOnAcid: CombinationFactory::REBOUND...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1111'
  original_post_id: '1453'
  _wp_old_slug: '1453'
---
Added a simple constraint type to CombinationFactory that causes values to "bounce" off of the upper and lower bounds:

<pre>
-0.2 -&gt; 0.2
-0.1 -&gt; 0.1
0.0 -&gt; 0.0
0.1 -&gt; 0.1
0.2 -&gt; 0.2
...
0.9 -&gt; 0.9
1.0 -&gt; 1.0
1.1 -&gt; 0.9
1.2 -&gt; 0.8
...
1.9 -&gt; 0.1
2.0 -&gt; 0.0
2.1 -&gt; 0.1
</pre>

So when scaled to screen dimensions, for example, x and y coordinates can seem to "rebound" off the edges of the screen, or an object can "bounce" back and forth between two colors, or minimum and maximum sizes.  The SineFactory did some of this before, but this gives an abrupt reversal of direction instead of a smooth curve (and sometimes the former looks cooler).

Also, I had the ExampleFactory randomly choose an operation and a constraint mode for its component CombinationFactory.  Since it only used the defaults before, and since it seems I never use any functionality that isn't wrapped up in the ExampleFactory, these rather cool features were woefully under-utilized.  This should fix that.

Here's a few sample SVG files, generated with the updated ExampleFactory:

<a href="http://jay.mcgavren.com/files/2010-11-09_232353.svg">2010-11-09_232353.svg</a>

<a href="http://jay.mcgavren.com/files/2010-11-09_232419.svg">2010-11-09_232419.svg</a>

<a href="http://jay.mcgavren.com/files/2010-11-09_232816.svg">2010-11-09_232816.svg</a>

<a href="http://jay.mcgavren.com/files/2010-11-10_011839.svg">2010-11-10_011839.svg</a>
