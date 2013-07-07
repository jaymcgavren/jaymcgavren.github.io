---
layout: post
title: Android 1.0 API impressions...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '930'
  original_post_id: '1059'
  _wp_old_slug: '1059'
---
What they're describing here might be applicable not just to mobile apps, but maybe applications in general.  Could this become the basis of an OS for a set-top box, game console, or desktop?

An Activity is a unit of action a user can initiate.  Though an Activity can be used as an application, it isn't the same concept; an Activity could be accessed from the menu of another Activity, for example.

The lifecycle of an activity is:
<dl>
	<dt>onCreate()</dt>
	<dt>onRestart()</dt>
		<dd>Called here after an application is stopped, not during its initial startup.</dd>
	<dt>onStart()</dt>
		<dd>Activity is becoming visible to user.</dd>
	<dt>onResume()</dt>
		<dd>Activity can interact with user.</dd>
	<dt>onPause()</dt>
		<dd>System is about to switch to another activity.</dd>
	<dt>onStop()</dt>
		<dd>Activity is no longer visible to user.  May be followed by onRestart() or onDestroy().</dd>
	<dt>onDestroy()</dt>
		<dd>During this method, if isFinishing() returns true, user requested finish.  Otherwise, system did.</dd>
</dl>
This model is cool because it requires that an app be ready to save its state for later reloading at any time.  An app that follows this setup properly will be ready for the user to switch activities, to reflect changes to the global config, or for the phone's battery to run low.

Notifications: I'm imagining this to be like Growl or Enso notifications.  Hope I'm right, but I haven't read far enough to know yet.

Background processes!!!  The inability of third-party apps to do this is my number one complaint about the iPhone.  I want a daemon that can initiate different processes when I walk into work, home, or school, and I think it simply isn't possible on iPhone.
