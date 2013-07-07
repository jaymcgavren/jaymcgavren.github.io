---
layout: post
title: '#songsincode #songsintests'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1039'
  original_post_id: '1256'
  _wp_old_slug: '1256'
---
In response to a Twitter meme...  Sarah McLachlan's "Ice Cream".

{% highlight ruby %}
require 'test/unit'

class TestYou < Test::Unit::TestCase
  def test_you
    you = Object.new
    ice_cream = Object.new
    assert you.love > ice_cream
    anything_else = Object.new
    assert you.love > anything_else
    here = ['a', 'b']
    here.each {|body| assert_respond_to(body, :fight)}
  end
end
{% endhighlight %}
