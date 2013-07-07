---
layout: post
title: wxRuby animation demo not quite working...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '687'
  _oembed_22ec9fc995f6ccda4b32a5c22bab67c5: '{{unknown}}'
  original_post_id: '724'
  _wp_old_slug: '724'
---
Posted this to the wxruby-users mailing list.  Let's see if anyone else has attempted anything like this.

<blockquote>
OK, I have a basic blit demo working (thanks to Alex Fenton for his reply, which I finally saw).

However, there's a great deal of "tearing" on the screen - flickering grey lines in the black background.  It looks like the blit isn't always complete when the screen refreshes.

Can anyone look at this and tell me what I might be doing wrong?  Any help would be most appreciated!

-Jay McGavren
http://jay.mcgavren.com/zyps
</blockquote>


<!--more-->

{% highlight ruby %}
require 'rubygems'
require 'wx'

class MyApp  [300, 300])
    frame.show

    #Offscreen drawing buffer.
    buffer = Wx::Bitmap.new(300, 300)

    #Displays drawing.
    window = Wx::Window.new(frame, :size => [300, 300])
    window.evt_paint do |event|
      window.paint do |dc|
        #Copy the buffer to the viewable window.
        buffer.draw do |buffer_dc|
          dc.blit(0, 0, 300, 300, buffer_dc, 0, 0)
        end
      end
    end

    #Animate.
    (1..40).each do |i|
      #Clear screen.
      buffer.draw do |surface|
        surface.pen = Wx::Pen.new(Wx::Colour.new(0, 0, 0), 0)
        surface.brush = Wx::BLACK_BRUSH
        surface.draw_rectangle(0, 0, 300, 300)
      end
      #Draw line.
      buffer.draw do |surface|
        surface.pen = Wx::Pen.new(
          Wx::Colour.new(128, 255, 128),
          3
        )
        surface.pen.cap = Wx::CAP_ROUND
        surface.draw_line(i, 0, i+100, 100)
      end
      #Update screen.
      window.refresh
      window.update
      sleep 0.1
    end

  end

end

app = MyApp.new
app.main_loop
{% endhighlight %}
