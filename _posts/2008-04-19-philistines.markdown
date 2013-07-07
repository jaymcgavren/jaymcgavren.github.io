---
layout: post
title: Philistines...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '787'
  original_post_id: '869'
  _wp_old_slug: '869'
---
<pre>
( 0.000, -0.028)
( 0.000, -0.083)
( 0.000, -0.167)
( 0.000, -0.278)
( 0.000, -0.417)
</pre>

Jay: Lookit!  The Body's falling!

Diana: It's green text.

Jay: But it's falling!  There's gravity!  And it's accelerating over time!

Diana: It's only falling 5 times.

Jay: I can extend the loop!

[Diana walks out of room, shaking head.]

{% highlight ruby %}
require 'chipmunk'

include CP

space = Space.new
space.gravity = Vec2.new(0, -100)
radius = 10.0
body = Body.new(10.0, moment_for_circle(15.0, 0.0, radius, Vec2.new(0, 0)))
ball = Shape::Circle.new(body, radius, Vec2.new(0, 0))
space.add_body(body)

5.times do
	space.step(1.0 / 60.0)
	puts body.p
end
{% endhighlight %}
