---
layout: post
title: A challenge!
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1099'
  original_post_id: '1422'
  _wp_old_slug: '1422'
---
30 minutes ago, I got this comment on my Ruboto on Acid post:

> LSD makes letters on a computer screen look as if they're dancing around and have a mind of their own. It's also entirely impossible to think logically enough to code while on it. I recommend you buy some acid and see how it's nothing like this at all. ;)

And here is my answer.  :)

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-94231-pm.png' title='screen-shot-2010-06-12-at-94231-pm.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-94231-pm.thumbnail.png' alt='screen-shot-2010-06-12-at-94231-pm.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-94109-pm.png' title='screen-shot-2010-06-12-at-94109-pm.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-94109-pm.thumbnail.png' alt='screen-shot-2010-06-12-at-94109-pm.png' /></a>

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-93947-pm.png' title='screen-shot-2010-06-12-at-93947-pm.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-93947-pm.thumbnail.png' alt='screen-shot-2010-06-12-at-93947-pm.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-93537-pm.png' title='screen-shot-2010-06-12-at-93537-pm.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-06-12-at-93537-pm.thumbnail.png' alt='screen-shot-2010-06-12-at-93537-pm.png' /></a>

<a href="http://www.youtube.com/watch?v=JeysoRKMdkY">video</a>

{% highlight ruby %}
#!/usr/bin/env ruby

require 'rubyonacid/factories/example'
require 'tk'

#This factory will be in charge of all drawing coordinates, colors, etc.
f = RubyOnAcid::ExampleFactory.new

#A skip factory, in charge of randomly resetting the meta factory.
resetter = RubyOnAcid::SkipFactory.new(:odds => 0.99)

#The window to draw to.
canvas = TkCanvas.new(:width => 400, :height => 400)
canvas.pack

#The line objects we create will be stored here.
shapes = []

letters = "woah, trippy, dude!".split(//)

#Create a thread to update the window while it's displayed.
Thread.abort_on_exception = true
Thread.new do
  loop do
    
    #Get red, green, and blue values for a color from the factory.
    #Format is #RRGGBB in hexadecimal (like HTML).
    color = sprintf("#%02x%02x%02x",
      f.get(:red, :max => 254).to_i,
      f.get(:green, :max => 254).to_i,
      f.get(:blue, :max => 254).to_i
    )
    
    #Create and store a line of the chosen color.
    #Get width and locations of the endpoints from the factory.
    shapes << TkcText.new(
      canvas,
      f.get(:x1, :max => 400),
      f.get(:y1, :max => 400),
      :text => f.choose(:text, letters),
      :font => TkFont.new(
        :size => f.get(:size, :min => 1, :max => 72).to_i,
      ),
      :fill => color
    )
    
    #If the resetter returns true, tell the ExampleFactory to reassign
    #its source factories to different keys.
    f.reset_assignments if resetter.boolean(:reset)
    
    #Delete the oldest line if we have accumulated too many.
    shapes.shift.delete if shapes.length > letters.length

  end
end

#Display the window.
canvas.mainloop
{% endhighlight %}
