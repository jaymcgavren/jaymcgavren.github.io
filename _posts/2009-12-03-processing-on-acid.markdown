---
layout: post
title: Processing on Acid...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1071'
  original_post_id: '1352'
  _wp_old_slug: '1352'
---
Got Ruby-Processing working with external libraries, so I can finally try it out with Ruby On Acid!  My problem was that I couldn't (or didn't know how to) set the ruby load path with ruby-processing's included "rp5" tool.  But on <a href="http://blog.marcchung.com/">Marc Chung</a>'s advice, I tried loading it into vanilla JRuby (had to do a small hack, but it worked).  From there I was able to set $RUBYLIB, include it from a gem, whatever.

It's <em>fast</em>, too, at least compared to wxRuby on MRI 1.8.7.  My dual-core MacBook can draw 3000 shapes a second without breaking a sweat.

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/12/picture-8.png' title='picture-8.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/12/picture-8.thumbnail.png' alt='picture-8.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/12/picture-7.png' title='picture-7.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/12/picture-7.thumbnail.png' alt='picture-7.png' /></a><a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/12/picture-6.png' title='picture-6.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/12/picture-6.thumbnail.png' alt='picture-6.png' /></a>

OK, so here's how to try it out yourself:

Save to acid_sketch.rb:

{% highlight ruby %}

require 'rubygems'
require 'ruby-processing'
require 'rubyonacid/factories/meta'
require 'rubyonacid/factories/combination'
require 'rubyonacid/factories/constant'
require 'rubyonacid/factories/flash'
require 'rubyonacid/factories/loop'
require 'rubyonacid/factories/random'
require 'rubyonacid/factories/repeat'
require 'rubyonacid/factories/sine'
require 'rubyonacid/factories/skip'

class Sketch < Processing::App

  def setup
    @f = create_factory
    @resetter = RubyOnAcid::SkipFactory.new(0.9999)
    background 0
    smooth
    ellipse_mode CENTER
    rect_mode CENTER
  end
  def draw
    10.times do
      fill(
        @f.get(:red, :max => 255),
        @f.get(:green, :max => 255),
        @f.get(:blue, :max => 255),
        @f.get(:alpha, :max => 255)
      )
      no_stroke
      ellipse(
        @f.get(:x, :max => width),
        @f.get(:y, :max => height),
        @f.get(:width, :max => 100),
        @f.get(:height, :max => 100)
      )
      @f.reset_assignments if @resetter.boolean(:reset)
    end
  end

  def create_factory

    random_factory = RubyOnAcid::RandomFactory.new

    source_factories = []
    #Loop factories loop from 0.0 to 1.0 (or 1.0 to 0.0 if the increment value is negative).
    source_factories << RubyOnAcid::LoopFactory.new(0.01)
    source_factories << RubyOnAcid::LoopFactory.new(-0.01)
    source_factories << RubyOnAcid::LoopFactory.new(0.001)
    source_factories << RubyOnAcid::LoopFactory.new(-0.001)
    #Constant factories always return the same value,
    source_factories << RubyOnAcid::ConstantFactory.new(rand)
    source_factories << RubyOnAcid::ConstantFactory.new(rand)
    source_factories << RubyOnAcid::FlashFactory.new(rand(100))
    #Sine factories produce a "wave" pattern.
    source_factories << RubyOnAcid::SineFactory.new(0.1)
    source_factories << RubyOnAcid::SineFactory.new(-0.1)
    source_factories << RubyOnAcid::SineFactory.new(0.01)
    source_factories << RubyOnAcid::SineFactory.new(-0.01)
    #A RepeatFactory wraps another factory, queries it, and repeats the same value a certain number of times.
    source_factories << RubyOnAcid::RepeatFactory.new(
      RubyOnAcid::LoopFactory.new(random_factory.within(:increment, -0.1, 0.1)),
      random_factory.get(:interval, :min => 2, :max => 100)
    )
    source_factories << RubyOnAcid::RepeatFactory.new(
      RubyOnAcid::SineFactory.new(random_factory.within(:increment, -0.1, 0.1)),
      random_factory.get(:interval, :min => 2, :max => 100)
    )
    #A CombinationFactory combines the values of two or more other factories.
    combination_factory = RubyOnAcid::CombinationFactory.new
    2.times do
      combination_factory.source_factories << source_factories[rand(source_factories.length)]
    end
    source_factories << combination_factory

    #The MetaFactory pulls requested value types from the other factories.
    meta_factory = RubyOnAcid::MetaFactory.new
    meta_factory.factory_pool = source_factories

    meta_factory

  end
end

Processing::SKETCH_PATH = ""

Sketch.new :title => "Ruby On Acid", :width => 800, :height => 600, :full_screen => false
{% endhighlight %}

<pre>
jay@dandelion:~/Projects/ruby-processing
$ sudo jruby -S gem install ruby-processing
jay@dandelion:~/Projects/ruby-processing
$ sudo jruby -S gem install rubyonacid
jay@dandelion:~/Projects/ruby-processing
$ jruby acid_sketch.rb
</pre>
