---
layout: post
title: OK, so it's not useful NOW...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '932'
  original_post_id: '1039'
  _wp_old_slug: '1039'
---
Added to "utility/enhancements.rb"...

{% highlight ruby %}
class String
	#Uses Windows Speech API to speak string.
	def speak
		require 'win32/sapi5'
		Win32::SpVoice.new.Speak(self.to_s)
	end
end

99.downto(1) {|n| "#{n} bottles of beer on the wall".speak}
{% endhighlight %}
