---
layout: post
title: Bort with Rails 2.3, Authlogic, and Cucumber
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1006'
  original_post_id: '1193'
  _wp_old_slug: '1193'
---
We have a series of small new projects coming at work, and I <em>hate</em> project setup.  We'd used Bort previously, but it uses Restful Authentication, and my boss was recommending Authlogic.  I also didn't want to have to set up Cucumber on five new code bases.

So, Git/GitHub being the wonderful platform it is, I forked the Bort repo and set to work:

<a href="http://github.com/jaymcgavren/bort/tree/master">Bort with Rails 2.3, Authlogic, and Cucumber</a>

...I might have done better starting from scratch.  Bits of Restful Auth kept disrupting my Authlogic setup, likewise Rails 2.2 code with 2.3.

But in the end I prevailed (I think).  There may still be odd errors lurking in there.  Those should be teased out by the many projects I hope to use it on, though.
