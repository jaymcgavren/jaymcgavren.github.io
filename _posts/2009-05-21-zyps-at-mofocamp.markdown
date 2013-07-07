---
layout: post
title: Zyps at MofoCamp
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1018'
  original_post_id: '1211'
  _wp_old_slug: '1211'
---
Zyps was one of two chosen topics for Mofocamp last night.  I wasn't really expecting that, so I was totally unprepared, but we piled into one of the breakout rooms and started hacking away.

I said Zyps was ideally suited for simulations or shooter-type games, and someone raised the idea of an Asteroids clone.  I said not only could it be done, but half the code was written already (ExplodeAction, WrapAround, ShootAction, etc.).  The only uncertain area was keyboard input (and 10 minutes of wxRuby research took care of that).

It was definitely not my cleanest work ever; we copied the entire Zyps repo since the last gem is so old, and ripped the entire contents of bin/zyps as a basis.  I didn't realize it was loading an empty environment from a YAML file, so when I wasn't answering questions I was trying to figure out why the Asteroid and Ship objects (coded by Andrew Bowerman and Roy VandeWater) I was dropping in were mysteriously disappearing.

Thanks in part to that, we were 40 minutes late for presentation time (which was OK because the Processing team left without presenting), but we finally had a working demo.  Lots more to be done, but not bad for two and a half hour's work.

<a href="http://github.com/dneighbors/mofocamp/tree/master">Code (in "zyps" subdir)</a>

<a href="http://wiki.github.com/dneighbors/mofocamp/zyps">Wiki</a>

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/05/zypseroids.png' title='Zypseroids'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/05/zypseroids.thumbnail.png' alt='Zypseroids' /></a>
