---
layout: post
title: Client, server, client environment, server environment...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '759'
  original_post_id: '830'
  _wp_old_slug: '830'
---
OK, here's part of what I'm thinking...

{% highlight ruby %}
#Ensure server is authority on object movement by default.
def test_server_movement_authority
	@server.start
	@client.connect
	@client_environment << @object
	server_object = find_matching_object(@object, @server_environment)
	#Move client object one way, server object another.
	@object.vector.pitch = 90
	server_object.vector.pitch = 180
	#Interact.
	@server_environment.interact
	#Ensure client location/vector matches server's anyway.
	assert_equal(@object.vector, server_object.vector)
	assert_equal(@object.location, server_object.location)
end
{% endhighlight %}

Basically the client runs its own environment to keep things looking smooth, but when the server finally gets back in touch with it (and it could be several seconds), any location and vector the server sends gets blown away on the client.  (It won't send all of them, just those within a given update area.)
