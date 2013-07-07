---
layout: post
title: SVG Tweets and HTML5 Canvas Tweets are both a bust...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1127'
  original_post_id: '1497'
  _wp_old_slug: '1497'
---
...A `data:` URL can hold everything fine, sure, but I can't get 'em under 140 characters (at least, not while doing anything exciting with them).  There's just too much boilerplate.  I'm under 256, at least!

<h1>Canvas - Rotate and Scale</h1>

Paste this into your address bar:

<pre>
data:text/html,&lt;canvas id='c' width='999' height='999'/&gt;&lt;script&gt;c=document.getElementById('c').getContext("2d");for(s=1;s&lt;99;s++){c.scale(1.1,1.1);c.rotate(4);c.fillText("☃",1,2)}&lt;/script&gt;
</pre>

Or, just <a href='http://jay.mcgavren.com/blog/wp-content/uploads/2012/09/canvas_scale_rotate.html' title='HTML5 Canvas: Rotate and Scale'>click this link</a>.

<h1>SVG - Animation</h1>

SVG animations are <b>EXCITING</b>!  (Or, in the wrong hands, seizure-inducing.)

Paste this into your address bar:

<pre>
data:image/svg+xml,&lt;svg xmlns='http://www.w3.org/2000/svg'&gt;&lt;g transform="translate(500,400)"&gt;&lt;text x='-15' y='5'&gt;SVG!&lt;animateTransform attributeName="transform" type="scale" values="0;99;0" dur="0.3s" repeatCount="99"/&gt;&lt;/text&gt;&lt;/g&gt;&lt;/svg&gt;
</pre>

Or, just <a href='/files/animate_transform.svg' title='SVG: animateTransform'>click this link</a>.

Well, it was a fun experiment, anyway.  And there may be techniques for shaving off a few bytes out there; I might cram something worthwhile into a tweet yet.
