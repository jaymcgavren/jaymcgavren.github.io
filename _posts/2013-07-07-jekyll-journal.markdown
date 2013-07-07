---
layout: post
title:  "From Wordpress and HTML to Jekyll and Markdown"
tags: []
status: publish
type: post
published: true
---

It took every bit as long as I feared to port everything, but this blog is now powered by Jekyll.  Of course, Jekyll couldn't host all my old content out of the box.  Here are the tweaks I made:

* Enabled [pagination](http://jekyllrb.com/docs/pagination/).
* [Disqus](http://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions) for comments.
* [Initializr](http://www.initializr.com/) HTML/CSS templates.
* I found the Maruku parser for Markdown was choking on my old embedded HTML, so I switched to Redcarpet via the [configuration](http://jekyllrb.com/docs/configuration/).
* Some posts linked to other posts, so I had to alter them to use Jekyll's [`baseurl`](http://jekyllrb.com/docs/upgrading/#baseurl).
* All my old code was in `<pre>` blocks, so I had to switch it to use [Jekyll syntax highlighting](http://jekyllrb.com/docs/templates/#code_snippet_highlighting).
* Initializr wrapped code snippets by default.  Adding a CSS style of `overflow: auto` made them scroll instead (if they were too wide for the page).
* [Mou](http://mouapp.com/) (OSX only) is a pretty sweet Markdown editor.  I'm just starting with it, but I already like it.

I'm glad to have this done.  The record of one's development career should not be trusted to something as brittle as a Wordpress database.  Plus, Markdown and Git are just how I work, now.  Maybe if the flow of writing is a little more natural, I'll get this thing updated more often.
