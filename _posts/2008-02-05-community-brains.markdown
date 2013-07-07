---
layout: post
title: Community brains...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '714'
  original_post_id: '764'
  _wp_old_slug: '764'
---
I read an interview of a Halo 2 developer eons ago, without which I probably wouldn't have gotten nearly as far as I have on Zyps.  It was chock full of good ideas on networking.

And now I'm using the AI bits as well...  He mentioned that the enemies had to "take turns thinking" due to the XBox's limited processing power.  Basically, an AI was given a few processor cycles to size up its situation and choose its action, which it would then dumbly perform until its next turn to "think".

Zyps is getting really slow when there are dozens of creatures with 5-7 behaviors each on the screen.  It's time to assess splitting up my processor time as well.

Right now the plan is to add Behavior#condition_frequency, which will take an integer.  If you set behavior.condition_frequency = 3, then every third update, it will get a chance to select a new group of targets to act on dumbly for the next 3 updates.

The problem with this is that if they're created simultaneously, every behavior where condition_frequency = 3 will be called <em>on the same update</em>, meaning the first two updates will be ultra-smooth, and the third slow as hell.

I think I have a way to spread things out evenly: assign an incrementing offset to each Behavior that will decide which update number it receives from those allocated to its update frequency.

Here's a prototype, with a Counter that shares its "brains" with all other Counters in existence:

<!--more-->

{% highlight ruby %}
LOOP_COUNT = 5

class Counter
	@@increment_offsets = Hash.new {|h, k| h[k] = 0}
	attr_accessor :increment_interval
	attr_accessor :increment_offset
	attr_accessor :value
	def initialize(increment_interval)
		@increment_interval = increment_interval
		@value = 0
		@increment_offset = @@increment_offsets[increment_interval]
		@@increment_offsets[increment_interval] += 1
		@increment_attempts = 0
	end
	def increment
		@increment_attempts += 1
		return @value unless (@increment_attempts + @increment_offset) % @increment_interval == 0
		@value += 1
	end
end

singles, doubles, triples = [], [], []
3.times do
	singles << Counter.new(1)
	doubles << Counter.new(2)
	triples << Counter.new(3)
end
LOOP_COUNT.times do |i|
	[singles, doubles, triples].each do |counters|
		counters.each do |counter|
			counter.increment
			puts [
				counter.increment_interval,
				counter.increment_offset,
				counter.value
			].join("|")
		end
	end
	puts "----------------------------"
end
{% endhighlight %}

...And the result.  Note how a counter where increment_interval = 1 gets updated every call, 2's get updated every other call, and 3's every third call.

<pre>
1|0|1
1|1|1
1|2|1
2|0|0
2|1|1
2|2|0
3|0|0
3|1|0
3|2|1
----------------------------
1|0|2
1|1|2
1|2|2
2|0|1
2|1|1
2|2|1
3|0|0
3|1|1
3|2|1
----------------------------
1|0|3
1|1|3
1|2|3
2|0|1
2|1|2
2|2|1
3|0|1
3|1|1
3|2|1
----------------------------
1|0|4
1|1|4
1|2|4
2|0|2
2|1|2
2|2|2
3|0|1
3|1|1
3|2|2
----------------------------
1|0|5
1|1|5
1|2|5
2|0|2
2|1|3
2|2|2
3|0|1
3|1|2
3|2|2
----------------------------
</pre>
