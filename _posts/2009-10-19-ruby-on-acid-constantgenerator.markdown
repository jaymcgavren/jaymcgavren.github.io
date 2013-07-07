---
layout: post
title: 'Ruby on Acid: ConstantGenerator...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1061'
  original_post_id: '1327'
  _wp_old_slug: '1327'
---
It seems obvious, in retrospect, that a little stability was needed with all this randomness...

{% highlight ruby %}
@f.factory_pool << RubyOnAcid::ConstantFactory.new(rand)
{% endhighlight %}

In the image below, one of the Y coordinates is hooked up to a ConstantGenerator whose get_unit() always returns 0.5, hence, always halfway down the screen.

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-1.png' title='picture-1.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-1.thumbnail.png' alt='picture-1.png' /></a>

Similarly:

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-6.png' title='picture-6.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-6.thumbnail.png' alt='picture-6.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-9.png' title='picture-9.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-9.thumbnail.png' alt='picture-9.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-8.png' title='picture-8.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-8.thumbnail.png' alt='picture-8.png' /></a>
