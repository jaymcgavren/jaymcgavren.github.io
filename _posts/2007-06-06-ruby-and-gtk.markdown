---
layout: post
title: Ruby and GTK...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '499'
  original_post_id: '500'
  _wp_old_slug: '500'
---
Spent the last couple days flipping back and forth through <a href="http://ruby-gnome2.sourceforge.jp/hiki.cgi?Ruby-GNOME2+API+Reference">the API docs for a Ruby GTK library</a> and <a href="http://svn.ggzgamingzone.org/cgi-bin/trac.cgi/browser/trunk/gtk-games/combat">the source code for somebody's C game</a>.  The result is a quick demo of tearing-free GTK animation in Ruby.

It still skips some frames, though.  Can't remember quite what I did to address this in Zyps...

<!--more-->

{% highlight ruby %}
require 'gtk2'
WIDTH = 400
HEIGHT = 300

#Create a window, and set program up to quit when it is closed.
window = Gtk::Window.new
window.signal_connect("delete_event") {false}
window.signal_connect("destroy") {Gtk.main_quit}

#Create a drawing area on the window.
canvas = Gtk::DrawingArea.new
canvas.set_size_request(WIDTH, HEIGHT)
window.add(canvas)
window.show_all

#Create an offscreen buffer to draw to.
buffer = Gdk::Pixmap.new(canvas.window, WIDTH, HEIGHT, -1) #-1 for color depth signals to use window's color depth.

#Whenever the drawing area needs updating...
canvas.signal_connect("expose_event") do

	#Copy buffer bitmap to canvas.
	canvas.window.draw_drawable(
		canvas.style.fg_gc(canvas.state), #Gdk::GC (graphics context) to use when drawing.
		buffer, #Gdk::Drawable source to copy onto canvas.
		0, 0, #Pull from upper left of source.
		0, 0, #Copy to upper left of canvas.
		-1, -1 #-1 width and height signals to copy entire source over.
	)
	
end

#A looping animation of a moving circle.
animation = Thread.new do
	while 1 do
		(1 .. WIDTH).each do |x|
			#Clear the background on the buffer.
			buffer.draw_rectangle(
				canvas.style.bg_gc(canvas.state),
				true, #Filled.
				0, 0, #Upper-left corner.
				WIDTH, HEIGHT #Lower-right corner.
			)
			#Draw the circle.
			buffer.draw_arc(
				canvas.style.fg_gc(canvas.state),
				true, #Filled.
				x, HEIGHT/2 -30, #Upper-left endpoint.
				60, 60, #Width, height.
				0, 64 * 360
			)
			
			#Request the display be re-drawn.
			canvas.queue_draw_area(0, 0, WIDTH, HEIGHT)
			#Slow animation down a bit.
			sleep 0.001
		end
	end
end

#Begin waiting for window events.
Gtk.main

{% endhighlight %}
