---
layout: post
title: Notes from Jay Philips on Adhearsion...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '997'
  original_post_id: '1181'
  _wp_old_slug: '1181'
---
One of the more exciting talks at MountainWest RubyConf...  Looks like I could have something simple running in a weekend.

Asterisk front end.
Native integration with Rails.
Project:
<pre>
	dialplan.rb:
		adhearsion {
			simon_game
		}
		sandbox {
			play "hello-world" #Sound file stored on server.
			menu "hello-world" do |link|
				link.adhearsion 1 #Dialpad number to press.
				link.foobar 2
			end
		}
	events.rb
	components/
		sandbox/
			sandbox.rb
			sandbox.yml
				username: dfsklh
				password: dafsjkh
		my_component/
	config/
	startup.rb
</pre>
