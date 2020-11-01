---
layout: post
title: 'My Ruby Notes from 2006'
tags: []
status: publish
type: post
published: true
meta:
---
A coworker found her notes from very, very early in her Ruby studies and shared them with the team. I was _certain_ I had some as well, but couldn't find them at the time. I just stumbled across them today.

The file date (yeah, I kept these in a .txt file) was from March 27, 2006. So this was a few months after the original demo of Rails - that was what made me finally hop on the Ruby bandwagon.

<!--more-->

```
Local variables, method parameters, and method names should all start with a
lowercase letter or with an underscore. Global variables are prefixed with a
dollar sign ($), while instance variables begin with an ``at'' sign (@). Class
variables start with two ``at'' signs (@@). Finally, class names, module names,
and constants should start with an uppercase letter.
--
Expression interpolation:
	name = "Grandma"
	puts "Goodnight, #{name}"
	puts "1 + 1 = #{1 + 1}"
--
Working with arrays:
	a = [ 1, 'cat', 3.14 ]   # array with three elements
	a[0] 	# 	1
	a[2] = nil
	a 	# 	[1, "cat", nil]
--
Creating empty arrays:
	empty1 = []
	empty2 = Array.new
--
%w is similar to Perl's qw().
	a = %w{ ant bee cat dog elk }
	a[0] 	# 	"ant"
	a[3] 	# 	"dog"
--
Hashes:
	instSection = {
	  'cello'     => 'string',
	  'clarinet'  => 'woodwind',
	  'drum'      => 'percussion',
	  'oboe'      => 'woodwind',
	  'trumpet'   => 'brass',
	  'violin'    => 'string'
	}
--
Hashes are indexed using the same square bracket notation as arrays.
	instSection['oboe'] 	# 	"woodwind"
	instSection['cello'] 	# 	"string"
	instSection['bassoon'] 	# 	nil
--
	if count > 10
	  puts "Try again"
	elsif tries == 3
	  puts "You lose"
	else
	  puts "Enter a number"
	end
	puts "Danger, Will Robinson" if radiation > 3000
--
	while weight < 100 and numPallets <= 30
	  pallet = nextPallet()
	  weight += pallet.weight
	  numPallets += 1
	end
	square = square*square  while square < 1000
--
	if line =~ /Perl|Python/
	  puts "Scripting language mentioned: #{line}"
	end
--
Blocks:
	{ puts "Hello" }       # this is a block
	do                     # and so is this
	  club.enroll(person)  # <
	  person.socialize     # <
	end                    # <
--
Once you've created a block, you can associate it with a call to a method. That
method can then invoke the block one or more times using the Ruby yield
statement.
	def callBlock
	  yield
	  yield
	end
	callBlock { puts "In the block" }
That produces: "In the block\nIn the block".
--
You can provide parameters to the call to yield: these will be passed to the block.
	def myRoutine
	  yield 1, 2
	end
	myRoutine { |x, y| puts "#{x}/#{y}"} #Prints 1/2
	myRoutine { |x, y| puts "#{x + y}"} #Prints 3
--
Code blocks are used throughout the Ruby library to implement iterators:
	a = %w( ant bee cat dog elk )    # create an array
	a.each { |animal| puts animal }  # iterate over the contents
	[ 'cat', 'dog', 'horse' ].each {|animal| print animal, " -- "} #Produces "cat -- dog -- horse -- ".
--
Ruby uses this mechanism in place of for loops:
	5.times {  print "*" } #"*****"
	3.upto(6) {|i|  print i } #"3456"
	('a'..'e').each {|char| print char } #"abcde"
--
Standard input:
	line = gets
	print line
	while gets           # assigns line to $_
	  if /Ruby/          # matches against $_
	    print            # prints $_
	  end
	end
--
The predefined object ARGF represents the input stream that can be read by a program.
	ARGF.each { |line|  print line  if line =~ /Ruby/ }
--
Classes:
	class Song
	  def initialize(name, artist, duration)
	    @name     = name
	    @artist   = artist
	    @duration = duration
	  end
	end
	aSong = Song.new("Bicylops", "Fleck", 260)
--
The inspect method 
This will print #<Song:0x2748240 @name="Bicylops", @duration=260, @artist="Fleck">
	puts aSong.inspect
--
The to_s method can render any object to a string.
This will print #<Song:0x2748240>
	puts aSong.to_s
to_s can be overridden:
	class Song
	  def initialize(name, artist, duration)
	    @name     = name
	    @artist   = artist
	    @duration = duration
	  end
	  def to_s
	    "Song: #{@name}--#{@artist} (#{@duration})"
	  end
	end
	aSong = Song.new("Bicylops", "Fleck", 260)
	puts aSong.to_s 	# 	"Song: Bicylops--Fleck (260)"
--
Inheritance:
	class KaraokeSong < Song
	  def initialize(name, artist, duration, lyrics)
	    super(name, artist, duration)
	    @lyrics = lyrics
	  end
	end
```
