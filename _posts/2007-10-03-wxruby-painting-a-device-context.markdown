---
layout: post
title: 'wxRuby: Painting a device context...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '624'
  original_post_id: '648'
  _wp_old_slug: '648'
---
We pass Wx::Window#paint a block which will be called with a device context to paint on.  Then we hook this into Wx::Window#evt_paint so it's called whenever a repaint is needed.

This is a bit simpler than Ruby-Gnome2 so far...


<!--more-->

{% highlight ruby %}
gems_loaded = false
begin
	require 'wx'
rescue LoadError
	if gems_loaded == false
		require 'rubygems'
		gems_loaded = true
		retry
	else
		raise
	end
end

class MyApp < Wx::App
	def on_init
		#Create the top window.
		frame = Wx::Frame.new(nil, :size => [300, 300])
		#Create a panel within it.
		view = Wx::Window.new(frame)
		#Create a grey pen, 5 pixels wide.
		pen = Wx::Pen.new(Wx::Colour.new(128, 128, 128), 5)
		#Set up a handler for paint events.
		view.evt_paint do |event|
			#Wx::Window#paint takes a block.
			#This will later be called with a device context to paint on.
			view.paint do |dc|
				dc.clear
				dc.pen = pen
				dc.draw_line(0, 0, 100, 100)
			end
		end
		#Show the window.
		frame.show
		return true
	end
end

app = MyApp.new
app.main_loop
{% endhighlight %}
