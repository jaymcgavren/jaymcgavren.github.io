---
layout: post
title: Ruboto On Acid...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1096'
  original_post_id: '1419'
  _wp_old_slug: '1419'
---
After dissecting the demos that come with Ruboto 0.2 and figuring out how to upload a library and runner script to an Android emulator (hint: "$ adb push . /sdcard/jruby/subdirname"), it only took an hour or so to create a working Ruby On Acid demo.  And what worked on the emulator immediately worked when uploaded to the phone.

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-05-31-at-31718-am.png' title='Ruby On Acid in Ruboto IRB'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/06/screen-shot-2010-05-31-at-31718-am.thumbnail.png' alt='Ruby On Acid in Ruboto IRB' /></a>

<!--more-->

{% highlight ruby %}
$: << 'rubotoonacid/lib'
require 'rubyonacid/factories/example'

require "ruboto.rb"

java_import "android.graphics.Color"
java_import "android.graphics.Paint"
java_import "android.graphics.Canvas"
java_import "android.graphics.Bitmap"
java_import "android.content.res.ColorStateList"
java_import "org.jruby.ruboto.RubotoView"

f = RubyOnAcid::ExampleFactory.new
resetter = RubyOnAcid::SkipFactory.new(:odds => 0.99)
bitmap = Bitmap.create_bitmap(400, 854, Bitmap::Config::ARGB_8888)
buffer = Canvas.new(bitmap)

module Ruboto
  java_import "org.jruby.ruboto.irb.R"
  Id = JavaUtilities.get_proxy_class("org.jruby.ruboto.irb.R$id")
end

$activity.start_ruboto_activity "$arcs" do

  setup_content do
    RubotoView.new(self)
  end

  handle_draw do |view, canvas|

    paint = Paint.new
    paint.stroke_width = f.get(:width, :max => 10)
    paint.color = Color.argb(
      f.get(:alpha, :min => 50, :max => 255),
      f.get(:red, :max => 255),
      f.get(:green, :max => 255),
      f.get(:blue, :max => 255)
    )
    paint.anti_alias = true

    buffer.drawLine(
      f.get(:x, :max => 400),
      f.get(:y, :max => 854),
      f.get(:x1, :max => 400),
      f.get(:y1, :max => 854),
      paint
    )
    canvas.draw_bitmap(bitmap, 0, 0, nil)

    f.reset_assignments if resetter.boolean(:reset)

    view.invalidate

  end

  handle_stop do
    bitmap.recycle
  end


end

{% endhighlight %}

I do get a "bitmap size exceeds VM budget" error after the fourth run or so of the script, which persists until Ruboto is unloaded from memory.  Calling Bitmap.recycle() in the handle_stop callback doesn't seem to help.  Gonna have to figure all that out before this is ready for prime time.  Pretty damn sweet considering I once doubted I could ever use Ruby on the phone, though.

<em>Update 2010-06-03:</em> At Charlie Nutter's request, I created an all-in-one script suitable for demoing.  <del datetime="2010-08-02T01:10:32+00:00">Point your phone here and open the link with Ruboto (0.2 or later), give it a moment to load, then choose Execute: acid.rb</del>  Startup is a bit slow; I'll have to see if that can be improved for future scripts.

<em>Update 2010-08-01:</em> Here's an updated version that uses touch input.  <a href="/files/acid.rb">Point your phone here and open the link with Ruboto (0.3.1 or later), give it a moment to load, then choose Execute: acid.rb</a>.
