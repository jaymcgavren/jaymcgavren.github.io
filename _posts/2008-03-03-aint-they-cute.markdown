---
layout: post
title: Ain't they cute?
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '741'
  original_post_id: '799'
  _wp_old_slug: '799'
---
{% highlight ruby %}
view = TrailsView.new(
	:width => WIDTH,
	:height => HEIGHT,
	:scale => 0.5,
	:origin => Location.new(-200, -100)
)
{% endhighlight %}

<a href='http://jay.mcgavren.com/blog/archives/799/798/' rel='attachment wp-att-798' title='scale_origin.PNG'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2008/03/scale_origin.png' alt='scale_origin.PNG' /></a>

This is another prerequisite to a 2D shooter.  Scrolling should be a matter of:

{% highlight ruby %}
View#origin.y -= SCROLL_RATE * clock.elapsed_time
{% endhighlight %}

Some kind of factory can spawn enemies from a YAML file as the player approaches them, and delete them after he passes them.
