---
layout: post
title: The Reference Games Manifesto
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1113'
  original_post_id: '1464'
  _wp_old_slug: '1464'
---
A couple nights ago, I was playing Score Rush, a twin-stick shooter on XBox, and thinking what an exemplary game it was.  Simple, but with highly polished gameplay.  Something that other designers and developers could stand to learn from.

That started me wishing there was an open-source game in each genre that was playable and fun, but was first and foremost a reference for developers to learn techniques from.  Web framework standards have reference implementations, why can't games?  All the needed infrastructure is out there - freely available game libraries in a variety of languages, GitHub and other source code sites for forking and improving on projects, and a great many motivated (but largely disorganized) open-source game developers.  What if we joined forces to make something bigger than any one game?

And so resulted this initial draft of The Reference Games manifesto:

<ul>
  <li>We seek to meet the needs of both casual and experienced gamers where possible.
<ul>
  <li>We believe that affordances for casual gamers should never be obstructive to experienced gamers.</li>
  <li>In the rare event that needs are mutually exclusive, we strive to provide for both markets through multiple configurations of the same game.</li>
</ul></li>
  <li>We prove our assertions through appropriate testing.
<ul>
  <li>Example: A/B testing to prove that a particular control scheme reduces player error.</li>
</ul></li>
  <li>Although we support innovation, we are a platform for sharing proven best practices first.
<ul>
  <li>The reference game codebases can be forked and customized, but only proven techniques usable by a wide audience should be incorporated into core reference games.</li>
</ul></li>
  <li>We value gameplay over graphics.
<ul>
  <li>The majority of maintenance and development time should be spent on game mechanics.</li>
  <li>We support users with low-power or low-cost hardware.</li>
  <li>We allow graphical improvements through abstracted rendering interfaces.</li>
</ul></li>
  <li>We are open.
<ul>
  <li>We do not rely on proprietary frameworks or formats that are not freely available or could become unavailable in the future.</li>
</ul></li>
  <li>We work with the tools most commonly used by the development community.
<ul>
  <li>While respecting the openness principle, we choose the tools and languages most widely used by game developers.</li>
</ul></li>
</ul>

I don't know if I'll have an opportunity to go anywhere with this, but it's something I'd love to see.  Any enterprising developers out there that want to take this and run with it?
