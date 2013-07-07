---
layout: post
title: 'Ruby Tweets!'
tags: []
status: publish
type: post
published: true
meta:
  original_post_id: '1378'
  _wp_old_slug: '1378'
---
<pre>
ruby -e "i=0;loop{puts ' '*(29*(Math.sin(i)/2+1))+'|'*(29*(Math.cos(i)/2+1)); i+=0.1}" #ruby
</pre>

<i>about 23 hours ago via web</i>

<pre>
ruby -rtk -e "w=TkCanvas.new(TkRoot.new{title:paint});w.pack.bind('B1-Motion',proc{|x,y|TkcOval.new(w,x,y,x+4,y+4)},'%x %y').mainloop" #ruby
</pre>

<i>about 3 hours ago via web</i>

<em>Almost</em> got this one short enough to tweet:

<pre>
ruby -rtk -e"v,w=0,0;a=[1]*9;c=TkCanvas.new;c.pack.bind('Motion',proc{|x,y|a&lt;&lt;TkcLine.new(c,v,w,v=x,w=y,:arrow=&gt;'last');a.shift.delete rescue 1},'%x %y').mainloop"
</pre>

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/02/picture-7.png' title='Ruby Tk'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/02/picture-7.png' alt='Ruby Tk' /></a>
