---
layout: post
title: A before_filter equivalent for general Ruby...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '922'
  original_post_id: '1049'
  _wp_old_slug: '1049'
---
I've been able to wrap individual methods in other calls via alias_method for a while now, but I've always done it by hand; been meaning to write something up to do it generically...  Well, I came across an ugly but effective bit of code from Tadayoshi Funaba in <em>Programming Ruby</em> that was easily adapted to do just what I need.

{% highlight ruby %}
require 'logger'
require 'utility'

class Test
	def initialize
		@logger = Logger.new(STDOUT)
	end
	def bar(baz, glarch)
		puts [baz, glarch].join('/')
	end
	def log(*args)
		@logger.info(args)
	end
	before :bar, :log ###Here's the magic line!
end

test = Test.new
test.bar(1, 2)
{% endhighlight %}

Outputs:

<pre>
$ ruby test.rb
I, [2008-09-10T09:44:07.371000 #3292]  INFO -- : [1, 2]
1/2
</pre>

...Thanks to that "before :bar, :log", log() automatically got called before bar() with the same arguments.

Here's the alteration to Module that does it:

{% highlight ruby %}
class Module
	private
		def before(wrapped_method, pre_method)
			module_eval <<-EOD
				alias_method :__#{wrapped_method.to_i}__, :#{wrapped_method.to_s}
				private :__#{wrapped_method.to_i}__
				def #{wrapped_method.to_s}(*args, &block)
					#{pre_method.to_s}(*args, &block)
					__#{wrapped_method.to_i}__(*args, &block)
				end
			EOD
		end
end
{% endhighlight %}

Module#after() should work similarly.

<!--more-->

I experimented with a declaration like this, but without as much success:

{% highlight ruby %}
intercept_calls :bar do |*args|
	@logger.info(args)
end
{% endhighlight %}

...it complains whatever variables or methods referenced in the block aren't defined, which I guess they aren't at the time the block is evaluated.  Well, I'm sure there's a workaround for that too.  Meanwhile, this is pretty similar to before_filter, which is good enough for Rails.
