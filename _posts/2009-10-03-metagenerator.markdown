---
layout: post
title: MetaGenerator...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1058'
  original_post_id: '1306'
  _wp_old_slug: '1306'
---
I'm getting an <em>insane</em> amount of variety out of very little code.

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-39.png' title='picture-39.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-39.thumbnail.png' alt='picture-39.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-38.png' title='picture-38.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-38.thumbnail.png' alt='picture-38.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-37.png' title='picture-37.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-37.thumbnail.png' alt='picture-37.png' /></a>

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-36.png' title='picture-36.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-36.thumbnail.png' alt='picture-36.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-34.png' title='picture-34.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/10/picture-34.thumbnail.png' alt='picture-34.png' /></a>

{% highlight ruby %}
require 'rubygems'
require 'wx'
require 'rubyonacid/factories/meta'
require 'rubyonacid/factories/flash'
require 'rubyonacid/factories/increment'
require 'rubyonacid/factories/loop'
require 'rubyonacid/factories/random'
require 'rubyonacid/factories/sine'
require 'rubyonacid/factories/skip'



class MyApp < Wx::App

  WIDTH = 480
  HEIGHT = 480

  def on_init
 
    @f = RubyOnAcid::MetaFactory.new
    @f.factories << RubyOnAcid::FlashFactory.new
    @f.factories << RubyOnAcid::LoopFactory.new
    @f.factories << RubyOnAcid::RandomFactory.new
    @f.factories << RubyOnAcid::SineFactory.new
    @f.factories << RubyOnAcid::SkipFactory.new
    
    @resetter = RubyOnAcid::SkipFactory.new(0.999)
    
    #Containing frame.
    frame = Wx::Frame.new(nil, :size => [WIDTH, HEIGHT])
    frame.show
 
    #Displays drawing.
    window = Wx::Window.new(frame, :size => [WIDTH, HEIGHT])
 
    #Animate periodically.
    t = Wx::Timer.new(self, 55)
    evt_timer(55) {animate(window)}
    t.start(33)
 
  end
 
  def animate(window)
     window.paint do |surface|
       surface.pen = Wx::Pen.new(
           Wx::Colour.new(
             @f.within(:red, 0, 255).to_i,
             @f.within(:green, 0, 255).to_i,
             @f.within(:blue, 0, 255).to_i,
             @f.within(:alpha, 50, 255).to_i
           ),
           @f.within(:width, 1, 5).to_i
       )
       surface.draw_line(
          @f.within(:x, 0, WIDTH).to_i,
          @f.within(:y, 0, HEIGHT).to_i,
          @f.within(:x2, 0, WIDTH).to_i,
          @f.within(:y2, 0, HEIGHT).to_i
       )
     end
     @f.reset_assignments if @resetter.boolean(:reset)
  end

end

app = MyApp.new
app.main_loop
{% endhighlight %}
