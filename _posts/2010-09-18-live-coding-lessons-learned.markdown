---
layout: post
title: Live-Coding Lessons Learned
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1106'
  original_post_id: '1445'
  _wp_old_slug: '1445'
---
I had a spectacular time live-coding on a visualizer for the third <a href="http://desertbloomphoenix.com/">Desert Bloom PHX</a> party tonight.  I learned a few lessons while doing it, though, which I thought I'd share while they're still fresh in my mind.  I'm hoping these will help anyone who needs to supply visuals for parties.


If you're randomly generating settings, some of them are gonna look like crap.  Code up a way to quickly serialize presets to disk that you can switch between when you have an audience.  (You probably don't need a file save dialog, just a save button.  Think "that's pretty, save that" and "load up the next preset, whatever it is".)

{% highlight ruby %}
def save_preset
    t = Time.new
    file_name = sprintf("%04d-%02d-%02d_%02d%02d%02d", t.year, t.month, t.day, t.hour || 0, t.min || 0, t.sec || 0)
    File.open(File.join(preset_directory, file_name), "w") do |file|
        file.print YAML.dump [source_factories, @assigned_factories]
    end
    file_name
end
def next_preset
    directory = Dir.open(preset_directory)
    files = directory.entries[2..-1]
    @preset_index = @preset_index ? @preset_index + 1 : 0
    @preset_index = 0 if @preset_index > files.length - 1
    path = File.join(preset_directory, files[@preset_index])
    source_factories, @assigned_factories = YAML.load_file(path)
    path
end
{% endhighlight %}

Turn key settings of your visualizer into a Web service or other network service.  I made the onscreen text and "next preset" functions (among others) accessible over the network, then used a script on my smartphone as a remote control, leaving me free to roam the room.  This also enables something as simple as control from a second terminal window on the same machine.

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/09/screen-2010-09-18-at-12412-am.png' title='screen-2010-09-18-at-12412-am.png'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/09/screen-2010-09-18-at-12412-am.thumbnail.png' alt='screen-2010-09-18-at-12412-am.png' /></a>

{% highlight ruby %}
class <<f
    attr_accessor :text, :text_separator, :max_font_size, :min_font_size, :reset_odds, :shape_type, :max_shape_count, :listen_url
    attr_accessor :max_size
end
{% endhighlight %}

<!--more-->

You have to take a bathroom break sometime.  Ensure there's an autopilot mode that keeps switching to fresh visuals.  You could engage it manually, but consider having it take over automatically anytime the display sits for too long.

Your core animation loop needs to be surrounded with a begin/rescue/end or try/catch block.  You'd be surprised what you can recover from and keep going (without a jarring interruption of visuals) if you use an alternate thread to restore working settings.  And of course, don't just discard the error, be sure to print it to STDERR or a log.

{% highlight ruby %}
loop do
    begin
        shapes << make_shape(f, canvas, color, f.shape_type)
    rescue Exception => e
        puts e.message, e.backtrace
    end
end
{% endhighlight %}

Be ready to launch a second instance of your visualizer while the first is still running.  That way if something goes wrong, you can start the backup while the first is still limping along, put it in position, and kill the first instance without an (excessively) jarring transition.  For me, this meant duplicate terminal tabs with the environment fully set up in both.

Your backup visualizer may want network ports or other resources the first is occupying.  Rescue a failure and fall back to a secondary port if you can (and if that fails, start up without remote control).

{% highlight ruby %}
begin
  DRb.start_service(f.listen_url, f)
rescue Exception => e
  puts e.message, e.backtrace
  begin
    DRb.start_service(f.backup_url, f)
  rescue Exception => e
    puts e.message, e.backtrace
  end
end
{% endhighlight %}

Jason Ayers, who used to make a living VJing parties, tells me he ran a second machine on an alternate video input.  (This was a video player, not a laptop, but the principle's the same.)  This let him preview video and effects, and switch to whichever machine had something cooler going at the time.  I'd imagine it would have the added benefit of providing an additional backup to switch to in case of program, cable, or hardware failure.


Hope these prove helpful to anyone considering live coding for an audience.  If you know from experience of something that needs to be added or altered, drop me a line!
