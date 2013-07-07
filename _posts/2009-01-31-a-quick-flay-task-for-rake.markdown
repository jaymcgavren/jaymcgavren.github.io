---
layout: post
title: A quick Flay task for Rake...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '990'
  original_post_id: '1168'
  _wp_old_slug: '1168'
---
The only other one I saw posted missed parts of the specified subfolders.  So here goes:

{% highlight ruby %}
begin
	require 'flay'
	desc "Run duplicate code analyzer"
	task :flay do
		output = `flay #{FileList["lib/**/*.rb", "app/**/*.rb"].join(' ')}`
		fail "Error #{$?}: #{output}" unless $? == 0
		puts output
	end
rescue LoadError => exception
	warn "Could not load flay - it might not be installed."
end
{% endhighlight %}
