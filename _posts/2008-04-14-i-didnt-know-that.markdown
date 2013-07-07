---
layout: post
title: I didn't know that!
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '781'
  original_post_id: '860'
  _wp_old_slug: '860'
---
I <em>really</em> need to re-read Chapter 22 of Programming Ruby, because there's all kinds of gory Ruby details that didn't stick the first time...

<blockquote>
A statement may have an optional rescue modifier followed by another statement (and by extension another rescue modifier, and so on). The rescue modifier takes no exception parameter and rescues StandardError and its children.
If an exception is raised to the left of a rescue modifier, the statement on the left is abandoned, and the value of the overall line is the value of the statement on the right.
</blockquote>

{% highlight ruby %}
values = [ "1", "2.3", /pattern/ ]
result = values.map {|v| Integer(v) rescue Float(v) rescue String(v) }
result # [1, 2.3, "(?mix:pattern)"]
{% endhighlight %}
