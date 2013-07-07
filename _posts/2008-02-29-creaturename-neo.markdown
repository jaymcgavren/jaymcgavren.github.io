---
layout: post
title: creature.name = ‘Neo'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '740'
  original_post_id: '796'
  _wp_old_slug: '796'
---
A huge feature I'd always meant to include in Zyps but had thus far left out: bullet time.  On a whim today, I tried adding it, and it took all of 2 minutes...

{% highlight ruby %}
class Clock
	def initialize
		@@speed = 1
		reset_elapsed_time
	end
...
	#Returns the time in (fractional) seconds since this method was last called (or on the first call, time since the Clock was created).
	def elapsed_time
		time = Time.new.to_f
		elapsed_time = time - @last_check_time
		@last_check_time = time
		elapsed_time * @@speed
	end
...
	#Speed at which all Clocks are operating.
	def Clock.speed; @@speed; end
	#Set speed at which all Clocks will operate.
	#1 is real-time, 2 is double speed, 0 is paused.
	def Clock.speed=(value); @@speed = value; end
{% endhighlight %}

So far it seems to Just Work, but I have a lot of unit testing ahead before I'll declare that with confidence.

One other enhancement I may try is the ability to set a Clock <em>instance's</em> speed in addition to the global speed.  So you could pick up a power-up and suddenly be moving twice as fast as your environment or some such.
