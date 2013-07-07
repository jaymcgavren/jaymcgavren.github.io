---
layout: post
title: Ruby tweets!
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1090'
  original_post_id: '1408'
  _wp_old_slug: '1408'
---
A while back I stumbled across a page of JAPHs, or Just Another Perl Hacker scripts.  This was an ongoing competition Perl users had years ago to print the phrase "Just Another Perl Hacker" in the most convoluted way possible, utilizing little-known tricks of the language.  They usually stuffed these mini-scripts into their Usenet signatures.  I had always admired JAPHs, and decided to try my hand at a Ruby version.  But I needed a forum, and I hadn't been on Usenet in years.

So what's the modern version?  Why, Twitter, of course!  The 140-character limit would provide an extra level of challenge, enough so that I didn't feel a need restrict myself to printing "Just Another Ruby Hacker".

I started simple, printing a wave to STDOUT.

> `ruby -e "i=0;loop{puts ' '*(29*(Math.sin(i)/2+1))+'|'*(29*(Math.cos(i)/2+1)); i+=0.1}"` <a href="http://twitter.com/search?q=%23ruby" title="#ruby" class="tweet-url hashtag" rel="nofollow">#ruby</a>
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/9515188834"><span class="published timestamp">11:35 PM Feb 22nd</span></a>

Copy-paste that to a terminal, and hit Enter.  (If you copy from Twitter, there's no need to worry about line breaks or the Favorite star; the browser strips them.)  You get something like this:

<pre>
               |||||||||||||||||||||||||||||||||||||||||||
                   ||||||||||||||||||||||||||||||||||||||||||
                       ||||||||||||||||||||||||||||||||||||||||
                          ||||||||||||||||||||||||||||||||||||||
                            ||||||||||||||||||||||||||||||||||
                             ||||||||||||||||||||||||||||||
                             |||||||||||||||||||||||||
                           |||||||||||||||||||||
                        ||||||||||||||||||
                     |||||||||||||||
                 ||||||||||||||
            ||||||||||||||
        |||||||||||||||
     ||||||||||||||||||
  |||||||||||||||||||||
|||||||||||||||||||||||||
||||||||||||||||||||||||||||||
 ||||||||||||||||||||||||||||||||||
   ||||||||||||||||||||||||||||||||||||||
       |||||||||||||||||||||||||||||||||||||||||
          ||||||||||||||||||||||||||||||||||||||||||
               |||||||||||||||||||||||||||||||||||||||||||
                   ||||||||||||||||||||||||||||||||||||||||||
                       ||||||||||||||||||||||||||||||||||||||||
                          |||||||||||||||||||||||||||||||||||||
                            ||||||||||||||||||||||||||||||||||
                             |||||||||||||||||||||||||||||
                             |||||||||||||||||||||||||
                           |||||||||||||||||||||
...
</pre>

Here's a more-readable version:

{% highlight ruby %}
#Have to initialize i before incrementing.
i=0;

#loop{} is a few characters less than 1000.times{}.
#People know where Ctrl-C is on their keyboards. :)
#Brackets cost less characters than do/end.
loop {

  #sin() and cos() range -1 to 1.
  #We change result to range 0 to 1.
  left_width = Math.sin(i) / 2 + 1
  wave_width = Math.cos(i) / 2 + 1

  #Indentation of wave's left side.
  print ' ' * (29*left_width)
  #Wave's width, which decides placement of right side.
  print '|' * (29*wave_width)

  print "n"

  #Increasing input for sin()/cos() makes wave undulate.
  i += 0.1

}
{% endhighlight %}

That's still among my favorites.  But anybody can use puts().  The next was more ambitious...

<!--more-->

> `ruby -rtk -e "w=TkCanvas.new(TkRoot.new{title:paint});w.pack.bind('B1-Motion',proc{|x,y|TkcOval.new(w,x,y,x+4,y+4)},'%x %y').mainloop"` <a href="http://twitter.com/search?q=%23ruby" title="#ruby" class="tweet-url hashtag" rel="nofollow">#ruby</a>
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/9555955421"><span class="published timestamp">7:26 PM Feb 23rd</span></a>

> <span class="entry-content">That's my entry for world's smallest paint program.
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/9555999848"><span class="published timestamp">7:27 PM Feb 23rd</span></a>

Again, let's unpack that:

{% highlight ruby %}
#The Tk GUI library.
#-rtk on the command-line version does the same thing.
require 'tk'

#To be honest I'm not sure why this block works as-is.
#I guess it's equivalent to :title => :paint?
window = TkRoot.new{title:paint}

#Create a canvas with the window as its parent.
canvas = TkCanvas.new(window)

#Fit everything into the canvas; won't display if we don't.
canvas.pack

#Set up a Proc to be called when dragging with mouse button 1.
canvas.bind('B1-Motion',

  #Draw an oval at the given coordinates.
  proc{ |x,y|
    TkcOval.new(
      canvas,
      x,y,
      x+4,y+4
    )
  },

  #This is a Tk thing, it specifies parameters to pass to the block.
  '%x %y'

)

#Start the GUI thread.
canvas.mainloop
{% endhighlight %}

I did a bunch of other Tk snippets, too.  Then I switched to Curses (which lets you present GUI-like environments in the shell) to change it up.  This one draws a Lissajous curve:

> `ruby -rcurses -e"include Curses;i=0;loop{setpos 12*(Math.sin(i)+1),40*(Math.cos(i*0.2)+1);addstr'.';i+=0.01;refresh}"` <a href="http://twitter.com/search?q=%23ruby" title="#ruby" class="tweet-url hashtag" rel="nofollow">#ruby</a>
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/10110115308"><span class="published timestamp">11:54 PM Mar 6th</span></a>

Once more with legibility:

{% highlight ruby %}
require 'curses'

#Saves us having to put "Curses." before every method call.
include Curses

i=0

#Looping forever keeps the Curses interface displayed.
loop {

  #Coordinates to draw at.
  x = Math.sin(i) + 1
  y = Math.cos(i * 0.2) + 1

  #Move 'pen' to the coordinates, scaling up to fill the terminal.
  setpos 12 * x, 40 * y

  #Draw a period.
  addstr '.'

  #A much larger increment would work just as well.
  #But this slows the drawing process so you can see the first pass.
  i += 0.01

  #Redraw the Curses screen.
  refresh

}
{% endhighlight %}

That was enough for graphical stuff.  I moved on to playing with the Ruby language itself...

> <a href="http://twitter.com/search?q=%23ruby" title="#ruby" class="tweet-url hashtag" rel="nofollow">#ruby</a>` -e'def f(o);o.methods.each{|n|m = o.method(n);puts %Q/#{m}:#{m[*[o]*m.arity.abs]}/ rescue 1};end;f 1;f "r";f [1]*9;f({:a=>1});f 1..9'`
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/11224127352"><span class="published timestamp">6:37 PM Mar 28th</span></a>

> <a href="http://twitter.com/search?q=%23ruby" title="#ruby" class="tweet-url hashtag" rel="nofollow">#ruby</a> That prior one-liner calls every method it can on an integer, string, array, hash, and range. Use with caution on other objects!
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/11224213046"><span class="published timestamp">6:39 PM Mar 28th</span></a>

> @<a class="tweet-url username" href="http://twitter.com/jamesbritt" rel="nofollow">jamesbritt</a> If Ruby is a sharp knife, then I just spent the afternoon waving it around. :)
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/11227652753"><span class="published timestamp">7:50 PM Mar 28th</span></a> <span>via web</span> <a href="http://twitter.com/jamesbritt/status/11202137919">in reply to jamesbritt</a>

Expanded code:

{% highlight ruby %}
#This method will call every instance method it can on an object.
#Don't use single-letter method names at home, kids!
def f(o)

  #Object#methods() gives a list of strings with the object's method names.
  o.methods.each{ |method_name|

    #Object#method() gives an actual Method object.
    method = o.method(method_name)

    #Method#arity() gives the number of required arguments.
    argument_count = method.arity

    #The number will be negative if there are additional optional arguments.
    #We don't have space to figure those out, so we throw the info away.
    argument_count = argument_count.abs

    #Try to pass the object to its own method as arguments.
    #Obviously this will fail for things like String#insert(int, String).
    #But what do you want? We've got 140 characters to work with here.
    arguments = [o] * argument_count

    #Method#[] is an alias for Method#call().
    #Obviously a lot of calls will fail due to faulty arguments.
    #So we use an inline rescue and throw the exception away.
    result = method.call(*arguments) rescue 'fail'

    #Display the method we tried to call, and the result we got.
    puts "#{method}: #{result}"

  }

end

#Print methods for an Integer...
f(1)
#...for a String...
f("r")
#...for an Array (of nine Integers)...
f([1]*9)
#...for a Hash...
f({:a=>1})
#...and for a Range.
f(1..9)
{% endhighlight %}

I don't blame you if you don't want to run this yourself; I did it in a VM the first time.  But it seems you can't do much harm with Integers and Hashes.  I got output like this:

<pre>
            ...
            #&lt;Method: String#to_sym&gt;:rr
            #&lt;Method: String#capitalize&gt;:Rr
            #&lt;Method: String(Enumerable)#max&gt;:rr
            #&lt;Method: Array#inspect&gt;:[1, 1, 1, 1, 1, 1, 1, 1, 1]
            #&lt;Method: Array#compact&gt;:111111111
            #&lt;Method: Array#&lt;&lt;&gt;:111111111[...]
            #&lt;Method: Array(Kernel)#clone&gt;:111111111111111111[...]
            #&lt;Method: Array#empty?&gt;:false
            ...
</pre>

Like the others, this one was meant for pasting into a shell (within a Rails project's root), but it didn't take immediate effect...  The `echo x >> config/environments/development.rb` appended the Ruby snippet to the development configuration file.  Then, you just wait for your victim to start a server...

> `echo ";class <<STDOUT;def write(*a);super(*a.map{|o|o.reverse});end;end#pair+=crazy">>config/environments/development.rb`
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/11370604841"><span class="published timestamp">8:01 AM Mar 31st</span></a>

> That last one's for the <a href="http://twitter.com/search?q=%23rails" title="#rails" class="tweet-url hashtag" rel="nofollow">#rails</a> people. :)
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/11370625564"><span class="published timestamp">8:02 AM Mar 31st</span></a>

> @<a class="tweet-url username" href="http://twitter.com/logan_barnett" rel="nofollow">logan_barnett</a> it creates an object-specific class for STDOUT (an IO object) and overrides write() (which all output passes through).
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/11384164852"><span class="published timestamp">1:01 PM Mar 31st</span></a> <span>via web</span>

Here's a plain Ruby script with the same effect...

{% highlight ruby %}
#Monkey patch the IO class, but only for the STDOUT object.
class <<STDOUT

  #IO#write() appends strings to the IO object.
  #(That's the console, in STDOUT's case.)
  #I learned later that write() takes only a single argument,
  #so the splatting and mapping stuff probably wasn't necessary.
  #You'd need it for methods with optional arguments, though.
  def write(*a)

    #Call the original write() method...
    super(

      #...but not before we reverse all the strings.
      *a.map{|o| o.reverse}

    )

  end

end

#All these pass through write()...
p 'pair+=crazy'
printf "n%03d", 1
puts "Hello, world!"
{% endhighlight %}

That outputs:

<pre>
"yzarc=+riap"
100
!dlrow ,olleH
</pre>

So of course, when your poor pair programmer goes to look at the Rails log in the console, you can stifle your laughter as they puzzle over output like this:

<pre>
$ ruby script/server
=&gt; Booting Mongrel
=&gt; Rails 2.3.3 application starting on http://0.0.0.0:3000
hcated ot d- htiw llaC &gt;=
revres nwodtuhs ot C-lrtC &gt;=
)dnuof_ton( tuoyal/seucser gniredneR
:)}teg:&gt;=dohtem:{ htiw "raboof/" sehctam etuor oN( rorrEgnituoR::rellortnoCnoitcA
]TEG[ )24:20:02 81-40-0102 ta 1.0.0.721 rof( xedni#rellortnoCnoitacilppA gnissecorP
</pre>

I did another version that <a href="{{ site.baseurl }}2010/04/10/cackle.html">piped everything through the "banner" command</a>.  :)  I'll let your twisted little minds think up other possibilities.

Squeezing all this logic into 140 characters is pretty demanding.  I wondered if I could use dynamic method calls to do shorthand...

> `ruby -e "def method_missing(*m);s=m.shift;method(methods.find{|n|n=~/^#{s}/})[*m];end;p 'XXzAzTTzq'.rev.sp(/z/).map{|l|l.sq.suc}.jo.sw"
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/12333813790"><span class="published timestamp">2:38 AM Apr 17th</span></a>


{% highlight ruby %}
#Re-define Object.method_missing().
def method_missing(*m)

  #The symbol for the failed method call.
  shorthand = m.shift

  #Arguments, if any, follow the method name.
  arguments = m

  #methods() gives all defined method names for the current object.
  method_names = methods

  #Find the first method where the shorthand matches the start of its name.
  #You'll have to supply enough of the method name to ensure it's unique.
  #Otherwise, you could call a different method with a similar name.
  full_method_name = method_names.find do |name|
    name =~ /^#{shorthand}/
  end

  #method() gives the actual method reference, given the name.
  method_reference = method(full_method_name)

  #Splatting the argument array ensures that if it's empty,
  #the methods will be called with no arguments.
  method_reference.call(*arguments)

end

p 'XXzAzTTzq'.
  rev.     #String#reverse()
  sp(/z/). #String#split()
  map{|l|  #Array#map()
    l.     #['q', 'TT', 'A', XX], in order
    sq.    #String#squeeze()
    suc    #String#succ()
  }.
  jo.      #Array#join('')
  sw       #String#swapcase()
{% endhighlight %}

Which is the most convoluted way imaginable to output:

    "Ruby"

So it looks like you can do shorthand, but unfortunately my implementation costs more characters than it saves.  I may revisit that someday and use the extra space to write a fully-functional webserver in a tweet.  :)

For the finale, let's go back to Tk...

> `ruby -rtk -e"include Math;c=TkCanvas.new.pack;r=99;0.step(r,0.03){|a|TkcArc.new(c,x=r*sin(a)+r,y=r*cos(a)*sin(0.9*a)+r,x+4,y+4)};c.mainloop"`
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/12337212850"><span class="published timestamp">4:42 AM Apr 17th</span></a>

> <span class="entry-content">That's adapted from Creative Graphics on the BBC Microcomputer, John Cownie, 1982. Shaving those last 3 characters off was REALLY hard. :P</span>
> 
> 
> <a class="entry-date" rel="bookmark" href="http://twitter.com/jaymcgavren/status/12337385969"><span class="published timestamp">4:47 AM Apr 17th</span></a>

You know most of my techniques by now, so I'll leave that tweet for you to decipher.  That tiny bit of code generates a surprisingly-complex Lissajous yarn ball:

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2010/04/lissajous_ball.png' title='Lissajous Yarn Ball'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2010/04/lissajous_ball.png' alt='Lissajous Yarn Ball' /></a>

So there you have it: the arguably useless art of Ruby Tweets.  I did <a href="http://www.google.com/search?q=%22ruby%20-e%22&amp;tbs=mbl:1">a search with Google's Twitter tool</a> and learned that I'm not the only one attempting stuff like this, although others' tweets are much less, um, frivolous.  But there's not a ton of material out there.  I think this is a fun challenge, and I'd be curious to see what others can come up with!

If you'd like to see more, be sure to <a href="http://twitter.com/jaymcgavren">follow me on Twitter</a>.  And if you do anything cool, <a href="http://twitter.com/?status=@jaymcgavren">drop me a line</a> so I can retweet it!
