---
layout: post
title: This will only be funny to me...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '709'
  original_post_id: '758'
  _wp_old_slug: '758'
---
<blockquote>
(12:54:15 PM) jay: If dbaccess.Date is descended from java.util.Date, this code should work, shouldn't it?
        dbaccess.Date oneSecondFromNow = new dbaccess.Date(dbaccess.Date.TO_SECOND);
        oneSecondFromNow.setTime((new Date()).getTime() + 1);
I'm getting the current second instead of one second in the future.
(12:57:15 PM) gary:  + 1000....getTime is milliseconds
(12:57:34 PM) jay: Duh.  OK, thanks.
</blockquote>
