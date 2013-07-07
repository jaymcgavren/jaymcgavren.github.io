---
layout: post
title: Why I hate code generators...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '831'
  original_post_id: '928'
  _wp_old_slug: '928'
---
From the rSpec 1.1.4 release notes:

<blockquote>
<a href="http://rubyforge.org/forum/forum.php?forum_id=24724">Note: we've removed the metaclass method from Object. There were some
generated specs that used it, and they will now break. Just replace the
metaclass call with (class &lt;&lt; self; self; end) and all will be well.</a>
</blockquote>
