---
layout: post
title: Well, that was easy.
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '919'
  original_post_id: '1043'
  _wp_old_slug: '1043'
---
I showed Diana the demo rails site I was working on for Jeremy, but she wasn't much impressed.  She used layman's terms, but in effect said she was sure the modelling and authentication work I'd done was very impressive, but that she couldn't really appreciate that if all she saw was a plain white screen with some forms on it.  Visual design is not my area, so I wasn't looking forward to the effort required to make something pretty.

Well, one visit to a CSS templates site later, I have something I can drop into my application.html.erb, a default.css I can drop in public/stylesheets, and a much prettier demo.  No sweeping revision of my entire code base, no GUI layout editors, and almost no hand-editing.  Better yet, all I have to do to make the site skinnable is say

<pre>&lt;%= stylesheet_link_tag(session[:user].style || "default") %&gt;</pre>

in the default layout, and add a style attribute to the User model.  (This last idea from Chad Fowler's <em>Rails Recipes</em>.) Pretty freakin' sweet.
