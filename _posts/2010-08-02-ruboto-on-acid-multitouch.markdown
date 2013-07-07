---
layout: post
title: Ruboto On Acid - Multitouch
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1102'
  original_post_id: '1436'
  _wp_old_slug: '1436'
---
Ruboto 0.3 added TouchListener to its event handlers.  Here's my experiment with adding multitouch input to the Ruby On Acid demo...

When it starts up (or the factory resets), all attributes are controlled by an ExampleFactory, meaning they'll randomly be assigned to LoopFactories, SineFactories, RandomWalkFactories, etc.  Touch the screen, though, and control of the drawing x/y position will be given to the touchscreen.  Touch in a second place, and control of random attributes will go to your second finger: r/g/b channel, opacity, width, or height.

<!--more-->

{% highlight ruby %}
java_import "android.content.pm.ActivityInfo"
java_import "android.content.Context"
java_import "android.graphics.Color"
java_import "android.graphics.Paint"
java_import "android.graphics.Canvas"
java_import "android.graphics.Bitmap"
java_import "android.graphics.RectF"
java_import "org.ruboto.embedded.RubotoView"

$activity.start_ruboto_activity "$acid" do


  handle_create do |bundle|
  end


  setup_content do
    $acid.set_requested_orientation(ActivityInfo::SCREEN_ORIENTATION_PORTRAIT)
    @f = RubyOnAcid::MetaFactory.new
    @f.source_factories << RubyOnAcid::ExampleFactory.new
    @resetter = RubyOnAcid::SkipFactory.new(:odds => 0.999)
    @input_factories = {}
    @input_factories[:touch] = RubyOnAcid::InputFactory.new
    @input_factories[:touch].source_factories << RubyOnAcid::ExampleFactory.new
    @input_factories.values.each {|factory| @f.source_factories << factory}
    reset_assignments
    RubotoView.new($acid)
  end


  handle_draw do |view, canvas|

    @bitmap ||= Bitmap.create_bitmap(view.get_width, view.get_height, Bitmap::Config::ARGB_8888)
    @buffer ||= Canvas.new(@bitmap)

    paint = Paint.new
    paint.color = Color.argb(
      @f.get(:alpha, :min => 50, :max => 255),
      @f.get(:red, :min => 50, :max => 255),
      @f.get(:green, :min => 50, :max => 255),
      @f.get(:blue, :min => 50, :max => 255)
    )
    paint.anti_alias = true
    
    x = @f.get(:x, :max => view.get_width)
    y = @f.get(:y, :max => view.get_height)
    x_radius = @f.get(:x_radius, :min => 5, :max => view.get_width / 2)
    y_radius = @f.get(:y_radius, :min => 5, :max => view.get_width / 2)
    rect = RectF.new(x - x_radius, y - y_radius, x + x_radius, y + y_radius)
    @buffer.draw_oval(rect, paint)
    
    canvas.draw_bitmap(@bitmap, 0, 0, nil)
    
    reset_assignments if @resetter.boolean(:reset)

    view.invalidate
    
  end

  
  def reset_assignments
    @input_factories[:touch].clear_assigned_keys
    @input_factories[:touch].clear_input_values
    @input_factories[:touch].clear_seen_values
    @f.reset_assignments
    @f.assign_factory(:x, @input_factories[:touch])
    @f.assign_factory(:y, @input_factories[:touch])
    @input_factories[:touch].assign_key(:x, :x_0)
    @input_factories[:touch].assign_key(:y, :y_0)
  end
  
  
  handle_touch_event do |event|
    0.upto 10 do |pointer_id|
      index = event.find_pointer_index(pointer_id)
      break if index == -1
      @input_factories[:touch].put("x_#{pointer_id}".to_sym, event.get_x(index))
      @input_factories[:touch].put("y_#{pointer_id}".to_sym, event.get_y(index))
    end
  end
  
end
{% endhighlight %}


As before, I've created an all-in-one script that inlines the entire Ruby On Acid library.  <a href="/files/acid_multitouch.rb">Point your phone here and open the link with Ruboto (0.3.1 or later), give it a moment to load, then choose Execute: acid_multitouch.rb</a>.
