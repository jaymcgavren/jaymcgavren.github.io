---
layout: post
title: Delayed require statements...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '757'
  original_post_id: '828'
  _wp_old_slug: '828'
---
I have a set of Ruby utility libraries in my home directory for my own use, and it's nice not to have to care how bloated it's getting.  Except that it was taking up to 10 seconds for even basic operations.

The main problem was my strategy of "require libraries first, ask questions later" (which is the exact opposite of my strategy when I intend to distribute something).  My goal was to load everything up so I didn't have to think about which modules I needed (or type their names).  But even if all I was calling was a little file slurping routine, I got date parsing and PStore and a bunch of other stuff I didn't need.

Moving my require statements within the methods that use them alleviated things quite a bit.  Ruby doesn't care when you load your modules, so why take the hit at startup?

{% highlight ruby %}
def Utility.clipboard
	require 'win32/clipboard'
	Win32::Clipboard.data
end
{% endhighlight %}

A similar strategy is working nicely with Rake.  I want to offer amenities like rSpec and ruby-prof tasks, but don't want to make them requirements.  So I don't even define the task until I load the library successfully:

{% highlight ruby %}
begin
	require 'spec/rake/spectask'
	desc "Run user stories"
	task :stories do
		FileList["stories/*.rb"].each {|f| ruby f}
	end
rescue LoadError => exception
	warn "Could not load rSpec - it might not be installed."
end
{% endhighlight %}

I've encountered acolytes of various languages who like to declare their dependencies right at the top of a file for all to see, and that's a good thing.  But dependency declaration is starting to move into the package your source comes in (gems, POMs, etc.), so I don't think it's such a big deal to have it in the source any more.  If anyone knows of a pitfall I'm missing, though, I'd be interested to hear about it.
