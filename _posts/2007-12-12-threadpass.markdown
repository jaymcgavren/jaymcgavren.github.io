---
layout: post
title: Thread.pass...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '694'
  original_post_id: '733'
  _wp_old_slug: '733'
---
zyps_demo is locking up the interface so that it won't respond to window close events until the demo is done.  The zyps executable itself will presumably lock up as well.  But via a Google search, Alex Fenton has (inadvertently) helped me out a second time...

<blockquote>
<a href="http://rubyforge.org/pipermail/wxruby-users/2007-April/003055.html">"using Wx::Timer + Thread.pass + evt_timer inside App#on_init seems to work well on OS X (dev, not 0.0.39), GTK (both) and Windows (both)."</a>
</blockquote>

The problem is present in my brief wxRuby test as well, so here's a revised version of that, which plays much nicer...


<!--more-->

{% highlight ruby %}
require 'rubygems'
require 'wx'

class MyApp < Wx::App

  def on_init

    #Animate every 55 seconds.
    t = Wx::Timer.new(self, 55)
    evt_timer(55) { Thread.pass }
    t.start(33)

    #Window/buffer setup code...

    #Animate.
    Thread.new do
      (1..300).each do |i|
        #Animation code...
      end
    end

  end

  #def update_window...

end

app = MyApp.new
app.main_loop
{% endhighlight %}
