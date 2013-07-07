---
layout: post
title: Quick HOWTO for Hirb formatter for irb/Rails console...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1045'
  original_post_id: '1271'
  _wp_old_slug: '1271'
---
<a href="http://tagaholic.me/2009/03/13/hirb-irb-on-the-good-stuff.html">Hirb</a> is pretty object formatting for irb (and the Rails console).  If squinting at the standard Object#inspect output is slowing you down (trust me, it is), you should look into Hirb.  Here's &lt;5 minute setup...

Install the gem:

<pre>sudo gem install hirb</pre>

Add these lines to your $HOME/.irbrc file, which will cause Hirb to be auto-loaded at startup for both irb and script/console:

{% highlight ruby %}
require 'rubygems'

require 'hirb'
extend Hirb::Console
Hirb::View.enable
{% endhighlight %}

Try it out in irb:

<pre>
$ irb
irb(main):001:0&gt; table ['foo', 'bar']
+-------+
| value |
+-------+
| foo   |
| bar   |
+-------+
2 rows in set
=&gt; true
irb(main):002:0&gt;
</pre>

Try it out in script/console:

<pre>
jay@dandelion:~/Projects/myproject
$ script/console
Loading development environment (Rails 2.3.2)
&gt;&gt; MyModel.all
+----+-----------------+-------------------------+-------------------------+
| id | name            | created_at              | updated_at              |
+----+-----------------+-------------------------+-------------------------+
| 1  | Foo             | 2009-06-16 23:38:10 UTC | 2009-06-16 23:38:10 UTC |
| 2  | Bar             | 2009-06-17 00:38:16 UTC | 2009-06-17 00:38:16 UTC |
+----+-----------------+-------------------------+-------------------------+
2 rows in set
</pre>

Hirb has customization options I haven't even begun to explore, so be sure to look at its docs.
