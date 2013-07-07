---
layout: post
title: Lazy Google...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '625'
  original_post_id: '649'
  _wp_old_slug: '649'
---
Made a slight improvement to the standard Google "Google Bookmark" bookmarklet (boy, there's a mouthful)...  It quotes the current selection and uses it as a description, a la Lazy Sheep for del.icio.us.

<a href='document.selection.createRange().text)+""","bkmk_popup","left="+((a.screenX||a.screenLeft)+10)+",top="+((a.screenY||a.screenTop)+10)+",height=420px,width=550px,resizable=1,alwaysRaised=1");a.setTimeout(function(){d.focus()},300)})();'>Google Bookmark</a>

Thanks to <a href="http://ejohn.org/projects/sheep/">John Resig</a> and <a href="http://www.niallkennedy.com/blog/archives/2006/01/google-bookmark.html">Niall Kennedy</a>.
