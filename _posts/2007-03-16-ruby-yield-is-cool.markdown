---
layout: post
title: Ruby yield is cool.
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  original_post_id: '446'
  _wp_old_slug: '446'
---
Before:

{% highlight ruby %}
	#Find playlist by name and add to list.
	if config.has_key?('playlist')
		config['playlist'].each do |name|
			playlists.push(interface.LibrarySource.Playlists.ItemByName(name))
		end
	end
	#Create playlist and add to list.  [Note the near-identical code.]
	if config.has_key?('create-playlist')
		config['create-playlist'].each do |name|
			playlists.push(interface.CreatePlaylist(name))
		end
	end
	#...etc.
{% endhighlight %}

After:

{% highlight ruby %}
	#Invoke a block with each of the values for the given option in the given configuration.
	def with_option_values (key, config)
		if config.has_key?(key)
			config[key].each do |value|
				yield value
			end
		end
	end
	#Find playlist by name and add to list.
	with_option_values('playlist', config) do |name|
		playlists.push(interface.LibrarySource.Playlists.ItemByName(name))
	end
	#Create playlist and add to list.
	with_option_values('create-playlist', config) do |name|
		playlists.push(interface.CreatePlaylist(name))
	end
{% endhighlight %}

...Two completely different operations, but with <i>yield</i> and blocks, I'm able to remove the boilerplate around them.  Multiply that across a dozen similar sections of code, and you start to see real readability improvements.
