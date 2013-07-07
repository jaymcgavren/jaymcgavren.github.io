---
layout: post
title: Notes from RailsConf - Getting to Know Ruby 1.9...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1011'
  original_post_id: '1201'
  _wp_old_slug: '1201'
---
Hosted by David A. Black

<pre>
1.8.6:
	&gt; Object.new.to_a
	[#&lt;Object...&gt;]
	&gt; "onentwonthree".to_a
	["onen", "twon",...]
1.9:
	&gt; (0..10).to_a
	[1, 2, ...]
	Above 1.8 items don't have .to_a, though.  After all, why *should* an object know how to wrap itself in an array?
	&gt; Array(Object.new) #Array now has the responsibility.
	[#&lt;Object...&gt;]
1.9:
	&gt; "abc".to_i
	0
	&gt; Integer("abc")
	Exception
1.8:
	&gt; {1, 2, 3, 4}
	Hash
1.9:
	&gt; {1 =&gt;2, 3 =&gt; 4}
	Have to use hash rockets.
1.8:
	&gt; String.ancestors
	[Enumerable, String, Comparable, ...]
	&gt; "1n2n3".each{|s| puts s}
	1
	2
	3
	&gt; "abcndefnghi".map {|s| s.reverse }
1.9:
	String does not mix in Enumerable
	&gt; "".each
	NoMethodError...
	&gt; "abcndefnghi".lines.each {|l| puts l.upcase}
	&gt; "abcndefnghi".each_line {|l| puts l.upcase} #Equivalent
	&gt; "abcndefnghi".bytes.each {|l| puts l.upcase}
	&gt; "abcndefnghi".code_points.each {|l| puts l}
1.9:
	&gt; str = "Give me 100u20ac"
	"Give me 100&lt;Euro symbol&gt;"
	&gt; str.bytes.to_a.size
	14
	&gt; str.chars.to_a.size #Shorter than .bytes due to Unicode character.
	12
1.8:
	&gt; str = "This isna three-nline string"
	str[6] #Gives the ordinal.  (Kinda hacky...)
	115
	&gt; str[6, 1]
	"s"
1.9:
	&gt; str = "Give me 100u20ac"
	&gt; str[2] #Gives the character (I like this better).
	"v"
	&gt; str[2].ord
	118
	&gt; str[2, 1]
	"v"
	&gt; str[2, 5]
	"ve me"
1.9:
	&gt; h = {:one =&gt; 1, :two =&gt; 2}
	&gt; h = {one: 1, two: 2, three: 3} #New hash separator!
1.9:
	&gt; link_to "click", controller: "users" #That's a hash as the last argument, braces are optional.
1.8:
	&gt; {1 =&gt; 2, 3 =&gt; 4, 5 =&gt; 6} #Non-deterministic, could give {5 =&gt; 6, 3 =&gt; 4}
1.9:
	&gt; {5: 6, 1: 2}.each {|k, v| p "#{k}: #{v}"} #Order is deterministic.
	5: 6
	1: 2
1.9:
	Beware: Hash#sort still returns an Array of Arrays, not a re-ordered Hash.  That may change.
	Hash#select still returns a Hash.
1.9:
	Enumerable module has new methods.
	&gt; a = (1 .. 10).to_a
	&gt; a.each_slice(3) {|slice| p slice}
	[1, 2, 3]
	[4, 5, 6]
	...
	[10]
1.9:
	&gt; a.each_cons(3) {|cons| p cons} #Moves result start by 1 index each time.
	[1, 2, 3]
	[2, 3, 4]
	[3, 4, 5]
1.9:
	&gt; a.one? {|i| i == 2}
	false
	&gt; a.all? {|i| i == 2}
	false
	&gt; a.any? {|i| i == 2}
	true
1.9:
	&gt; ('a'..'c').cycle(2)
	#&lt;Enumerator&gt;
	&gt; ('a'..'c').cycle(2).to_a
	['a', 'b', 'c', 'a', 'b', 'c']
	.cycle with no args loops forever.  Fun, but dangerous.
1.8:
	&gt; x = 1
	&gt; [10, 20, 30].each {|x| puts x * 100}
	1000
	2000
	3000
	&gt; x == 30
	true #WTF?  Why not 1?  Wasn't x in the block scoped only to the block?
	&gt; [10, 20, 30].each {|@var| puts @var}
	10
	20
	30
	&gt; @var
	30
1.9:
	&gt; x = 1
	&gt; [10, 20, 30].each {|x| puts x * 100}
	1000
	2000
	3000
	&gt; x
	1 #There we go, it wasn't overwritten.
	[1, 2, 3].each {|@x|}
	SyntaxError: formal argument cannot be an instance variable.  (That's a good thing to me.)
</pre>
