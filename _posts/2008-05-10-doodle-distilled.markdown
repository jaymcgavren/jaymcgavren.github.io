---
layout: post
title: Doodle, Distilled...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '817'
  original_post_id: '906'
  _wp_old_slug: '906'
---
Gonna give a brief presentation on <a href="http://doodle.rubyforge.org">Doodle</a> to the Ruby Users Group on Monday.  While some folks can just wing it, I needed to prepare notes.  The need for brevity and a large font for the projector requires a short and sweet summary.

In hopes of helping others, here's what I've got...

<!--more-->

{% highlight ruby %}
#The old, painful way...

class Person
	attr_accessor :name, :age, :occupation
	def initialize(name, options = {})
		options = {
			:age => 30
		}.merge(options)
		@name = name
		@age = options[:age]
		@occupation = options[:occupation]
	end
end

p Person.new('Matz', :occupation => 'Minor Deity')


#The new, improved way:

require 'rubygems'
require 'doodle'

class Animal < Doodle
	has :age
end

p Animal.new(:age => 'Sparky')


#Wait, that's not quite right.
class Animal < Doodle
	has :age, :kind => Numeric
end
begin
	p Animal.new(:age => 'Sparky')
rescue Exception
	p $! #Animal.age must be Numeric...
end
#Much better.
p Animal.new(:age => 3)


#Other ways:
p Animal 4
p Animal :age => 5
p Animal {age 6}


#All attributes are required...
begin
	p Animal.new
rescue Exception
	p $! #missing required attribute 'age'
end
#Unless an initial value is given...
class Animal < Doodle
	has :age, :init => 1
end
p Animal.new


#"must" lets you validate with a block.
class Animal < Doodle
	has :birthdate, :kind => Date do
		must "not be in future" do |value|
			value <= Date.today
		end
	end
end
begin
	p Animal.new(
		:birthdate => Date.parse('2999-12-31')
	)
rescue Exception
	p $! #Animal.birthdate must not be in future
end
p Animal.new(:birthdate => Date.parse('1999-12-31'))


#Collectors let you add items to a collection.
class Goose < Doodle
	has :name
end
class Flock < Doodle
	has :geese, :init => [], :collect => Goose
end
flock = Flock do
	goose "Rebeccah"
	goose "Jemima"
end
p flock.geese


#There's more:
#http://doodle.rubyforge.org/
#sudo gem install doodle
{% endhighlight %}
