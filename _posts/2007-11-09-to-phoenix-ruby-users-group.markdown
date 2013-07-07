---
layout: post
title: 'To: Phoenix Ruby Users Group'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '670'
  original_post_id: '698'
  _wp_old_slug: '698'
---

<blockquote> From: James Britt
Date: Nov 6, 6:23 pm
Subject: November Phoenix Ruby User Group Meeting (PLEASE NOTE NEW LOCATION!)
To: Phoenix Ruby Users Group

November Phoenix Ruby User Group Meeting

Date:  Monday, November 12, 2007
Time:  7:00pm
Place: Rising Tide Software

...

Topics:

* A recap of the recent RubyConf 2007
by people who were *Actually There!*
<b>* A demo of the Zyps game library by Jay McGavren!</b>
* Maybe some other stuff!</blockquote>

I prepped a tutorial on the dRuby server, which I've copied here...


<!--more-->

First, install Zyps:

<pre>sudo gem install zyps</pre>

Run Ruby in interactive mode:

<pre>irb</pre>

Load the libraries for remote communication:

<pre>require 'rubygems'
require 'zyps/remote'
include Zyps</pre>

Set up a proxy to the remote environment:

<pre>uri = 'druby://lappy486:8989'
environment = EnvironmentClient.get_environment(uri)</pre>

Create a creature:

<pre>creature = Creature.new
creature.location = Location.new(200, 100) #x, y
creature.vector = Vector.new(45, 50) #angle, speed
creature.size = 50</pre>

Add it to the environment:

<pre>environment.objects &lt;&lt; creature</pre>

Let's make one that actually does something.

A Behavior has one or more Actions.

<pre>chase = Behavior.new
chase.actions &lt;&lt; ApproachAction.new(360, Vector.new(50, 0))</pre>

Copy our first Creature...

<pre>cat = creature.copy</pre>

This cat will be orange...

<pre>cat.color = Color.new(1, 0.75, 0)</pre>

Add the Behavior...

<pre>cat.behaviors &lt;&lt; chase</pre>

And add it to the environment.

<pre>environment.objects &lt;&lt; cat</pre>

Add a few more...

<pre>5.times {|i| environment.objects &lt;&lt; cat.copy}</pre>

Behaviors also have Conditions.

These limit the circumstances under which Actions occur.

Let's make a timid Creature that flees when others get too close.

<pre>run = Behavior.new
run.actions &lt;&lt; FleeAction.new(360, Vector.new(60, 0))
run.conditions &lt;&lt; ProximityCondition.new(200)</pre>

Copy a creature...

<pre>mouse = creature.copy
mouse.size = 10</pre>

Add the Behavior...

<pre>mouse.behaviors &lt;&lt; run</pre>

And add several to the Environment.

<pre>5.times {|i| environment.objects &lt;&lt; mouse.copy}</pre>

EnvironmentalFactors affect all the objects at once.

Let's mix it up and add some wind.

<pre>environment.environmental_factors &lt;&lt; Accelerator.new(Vector.new(200, 0))</pre>

There are many other Actions, Conditions, and EnvironmentalFactors to play with.  Read about them in the API docs:

<a href="http://jay.mcgavren.com/zyps_doc/">http://jay.mcgavren.com/zyps_doc/</a>
