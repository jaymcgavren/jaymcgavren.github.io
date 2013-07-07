---
layout: post
title: Linux is a jealous OS...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  original_post_id: '146'
  _wp_old_slug: '146'
---
My Ubuntu install has gone very well so far, with one major hiccup - it rendered my Windows installation unbootable.

During the setup process, while it was installing a boot loader (which lets you choose an OS and loads it up), it informed me that it "should be OK" to place the loader on the Master Boot Record (the first place on a disk that gets accessed when booting).  Not knowing enough to say otherwise, I let it do so.  It was only later that I found out that Windows refuses to boot from any partition except the MBR.  &gt;:(  (I'm just as mad at Windows as I am at Ubuntu.)

So my Windows install is nuked, and I can't restore it unless I wipe the hard drive clean.

Now I have two choices.  One, I can spend the next week backing up my 90 GB media partition so I can clear my hard drive, then reinstall Windows and try to reconfigure it.  Two, I can try to learn the guts of Linux well enough to configure that.

None of this would be a problem if I didn't have a vacation coming up in two weeks that I was planning to spend developing.  Halo 2 will be taking up all my free time this week, leaving just one week to learn an OS, configure it so it's suitable for development work, refresh myself on Java, and learn the Java Web Services framework, or risk wasting the whole vacation.  Tough to do when you only have hours of free time each week.

P.S.: Linux is *much* faster than Windows.  I do think this will all be for the best in the long run.
