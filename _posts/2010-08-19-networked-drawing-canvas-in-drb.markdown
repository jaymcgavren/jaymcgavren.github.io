---
layout: post
title: Networked Drawing Canvas in DRb
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1104'
  original_post_id: '1438'
  _wp_old_slug: '1438'
---
In honor of Why The Lucky Stiff's contributions to the fun side of the Ruby community, <a href="http://whyday.org/">whyday.org</a> includes a challenge to "see how far you can push some weird corner of Ruby".  I can think of few corners of Ruby that are weirder (or more fun) than DRb.

Distributed RuBy (DRb) is, in my opinion, the most underrated portion of the Ruby standard library.  It lets you take a Ruby class and network-enable it with almost no additional code (and without modifying the original class).  Back in 2006 when I was considering whether to learn Ruby or not, I took one look at DRb and realized that a language that made such things possible was probably a language worth knowing.

I made this screencast to show off how powerful DRb is, and how easy it is to get started.  We create a simple drawing canvas in Tk, then use DRb to network-enable it and draw to it from a 4-line client.  We finish with a Ruby client that runs on Android via the Ruboto environment.  And along the way, we cover a little basic security to help keep you safe (this is a network app, after all).

[http://www.youtube.com/watch?v=Ca6CBm4bSU8](http://www.youtube.com/watch?v=Ca6CBm4bSU8)

Here's the complete code for the server:

{% highlight ruby %}
require 'tk'
require 'drb'

$SAFE = 1

canvas = TkCanvas.new(:width => 800, :height => 600)
canvas.pack

class RemoteCanvas
  def initialize(canvas)
    @canvas = canvas
  end
  def circle(x, y)
    TkcOval.new(@canvas, x, y, x + 40, y + 40)
  end
end

DRb.start_service("druby://192.168.0.100:9000", RemoteCanvas.new(canvas))

canvas.mainloop
{% endhighlight %}


Here's our (tiny) sample client:


{% highlight ruby %}
require 'drb'
DRb.start_service
canvas = DRbObject.new(nil, "druby://192.168.0.100:9000")
canvas.circle(300, 400)
{% endhighlight %}


And here's the complete touchscreen client for Ruboto:


{% highlight ruby %}
require "ruboto.rb"
confirm_ruboto_version(4, false)
java_import "org.ruboto.embedded.RubotoView"

require 'drb'
DRb.start_service

$activity.start_ruboto_activity "$druby" do

  setup_content do
    @service = DRbObject.new(nil, "druby://192.168.0.100:9000")
    RubotoView.new($druby)
  end

  handle_touch_event do |event|
    @service.circle(event.get_x, event.get_y)
  end

end
{% endhighlight %}


Enjoy, and of course feel free to post questions and comments below.  And if you're looking for your own way to celebrate WhyDay, why not pick <em>your</em> favorite library and network-enable it?
