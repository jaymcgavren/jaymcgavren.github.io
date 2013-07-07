---
layout: post
title: ActiveSupport, only when you need it...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '942'
  original_post_id: '1078'
  _wp_old_slug: '1078'
---
I'm betting Rails enthusiasts would like to have access to ActiveSupport core extensions all the time, even when working in regular Ruby.  But on my box, "require 'activesupport'" incurs a 6-10 second delay, so I don't really want to load it every time I bring up irb.

So I'm putting this in my Utility package:

{% highlight ruby %}
module DeferredActiveSupport
	def method_missing(method, *arguments, &block)
		require 'activesupport'
		if self.respond_to?(method)
			self.send(method, *arguments, &block)
		else
			raise NoMethodError.new("#{method} not defined")
		end
	end
end

class String
	include DeferredActiveSupport
end

class Object
	include DeferredActiveSupport
end

#Other classes as desired...
{% endhighlight %}

Which lets me do this:

{% highlight ruby %}
puts ({:foo => 'bar', :baz => 'glarch'}).to_json
puts 'foo'.titleize
puts 'test'.pluralize
puts 'large_pepperoni_pizza'.camelize
{% endhighlight %}

Yielding:

<pre>
{"foo": "bar", "baz": "glarch"}
Foo
tests
LargePepperoniPizza
</pre>
