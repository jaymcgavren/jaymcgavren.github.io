---
layout: post
title: Album version...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1042'
  original_post_id: '1259'
  _wp_old_slug: '1259'
---
#songsincode

{% highlight ruby %}
class Bitch
  def love(person)
    puts person
  end
end
bitches = [Bitch.new, Bitch.new, Bitch.new]

me = Object.new
me.instance_eval {def rock; 'the projects'; end}

bitches.each do |bitch|
  bitch.love(me) if me.respond_to? :rock
end

{% endhighlight %}
