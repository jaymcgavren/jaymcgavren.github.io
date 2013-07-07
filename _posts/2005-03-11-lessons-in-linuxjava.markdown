---
layout: post
title: Lessons in Linux/Java...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  original_post_id: '224'
  _wp_old_slug: '224'
---
Well, <a href="http://sourceforge.net/projects/tivoslideshow/">TivoSlideshow</a> is up and running on the Tivo itself finally, and it's handling both images and MP3s.  I've just turned it loose on my massive collections to see if any of my files will crash it.

A sampling of the lessons I learned this evening:

<ul>
<li>A shell script won't run if it contains DOS-style line separators.</li>
<li>"dos2unix" isn't installed by default; you have to install the "sysutils" package (a 30-second operation once you know you need it).</li>
<li>The JAVA_HOME and CLASSPATH environment variables need to be set before anything will compile on Java, and the Linux installer doesn't seem to do it for you.</li>
<li>Using getScaledInstance() on an image with Image.SCALE_DEFAULT looks really crappy.</li>
</ul>

Troubling and random problems, but I conquered them all with Google's help.
