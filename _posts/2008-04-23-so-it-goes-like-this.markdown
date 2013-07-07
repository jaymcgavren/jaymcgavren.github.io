---
layout: post
title: So it goes like this...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '793'
  original_post_id: '875'
  _wp_old_slug: '875'
---
Environment1
EnvironmentServer observes Environment1
Environment2
EnvironmentClient observes Environment2
Add Object1 to Environment1
Environment1 notifies EnvironmentServer of new Object1
EnvironmentServer sends Object1 to EnvironmentClient
EnvironmentClient adds Object1 to Environment2
<em>Environment2 notifies EnvironmentClient of new Object1
EnvironmentClient sends Object1 to EnvironmentServer</em>

<em>Screeeeee...</em>  Hold the phone.  I just created a loop of object additions there.

The problem is that Environments are set up to notify their observers whenever an object is added, even if it came from that observer.

What I <em>need</em> is an entirely different model.  Something that monitors the difference between two Environments, and then does the needed steps to synchronize them.  Like a diff or an rsync or something.

I need to draw some diagrams or browse some source code or something, 'cause an elegant solution eludes me.
