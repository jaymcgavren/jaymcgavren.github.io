---
layout: post
title: twtr is gud
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '858'
  original_post_id: '962'
  _wp_old_slug: '962'
---
<a href="http://twtr.rubyforge.org">This</a> should save me some coding...

<pre>
jmcgavre@JMCGAVREN:C:work
$ gem install twtr
Bulk updating Gem source index for: http://gems.rubyforge.org
Install required dependency highline? [Yn]  y
Successfully installed twtr-0.1.4
...

jmcgavre@JMCGAVREN:C:work
$ twtr setting
&gt;&gt; C:/Documents and Settings/jmcgavre/twtr/twtr.yml
Edit twtr config? [y/N]:y
Twitter username: jaymcgavren
...

jmcgavre@JMCGAVREN:C:work
$ twtr ft
jaymcgavren: @kstaken You should have Twitter SMS your phone so that you can never escape from it. :) (I'm not reading much either.)
joshknowles: Should I be using git pull --rebase &amp; git push or should I doing my development on a branch and pulling/merging with master?
...

jmcgavre@JMCGAVREN:C:work
$ twtr rp
chrismatthieu: @jaymcgavren you rock!  The htmlentities ruby gem was *exactly* what I needed!  Thank you.
joshknowles: @jaymcgavren thanks!


jmcgavre@JMCGAVREN:C:work
$ twtr up -m "Testing twtr command line client (sudo gem install twtr)... Nice so far."
jaymcgavren: Testing twtr command line client (sudo gem install twtr)... Nice so far.
jaymcgavren: @kstaken You should have Twitter SMS your phone so that you can never escape from it. :) (I'm not reading much either.)
...

</pre>

API available for all the above, too.
