---
layout: post
title: A time-sink is born...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '839'
  original_post_id: '936'
  _wp_old_slug: '936'
---
Found an old e-mail to my brother that is basically the inception of Zyps.  Not sure of the exact date, because dates got eaten by a corrupted mbox file eons ago.  Whenever Wired profiled the MIT Ants project, I guess.

<!--more-->

<blockquote>
Well, I have most of a skeletal class designed. The objects will currently let others modify their HP, velocities, etc., no questions asked, but we can easily add more rules now on an attribute-by-attribute basis. Now I just need to write a hasty framework to create some instances of the objects, and give them initial test locations and vectors.

But to be honest, that doesn't accomplish much. I mean, there won't even be a *ground*, and when there is, we have no way to detect a collision with it to prevent object from falling through it. When I think of what portion of the problem I can tackle next, I'm left casting about for a place to start.

At the forefront of the problem is my decidedly weak grasp of classes and their interactions. So I'd like to propose a 1-2 week tangent here, which will strengthen our skills and leave us with the satisfaction of a completed and fun little side project.

You'll like this one, because it has its roots in a robotics project at MIT. First of all, go here:
http://www.ai.mit.edu/projects/ants/
Basically the Ants are autonomous Hot Wheels cars armed with only a handful of sensors and an LED transmitter/reciever. Yet they can play all kinds of cool "games" like Follow the Leader and Tag.

Follow The Leader works like this: Each Ant transmits a unique ID signal, we'll say 1, 2, 3... etc. Ant 1 goes wherever the hell it pleases. Ant 2 is programmed to home in on Ant 1. Ant 3 is programmed to home in on Ant 2, and so forth. With this exceedingly simple behavior, what you wind up with is a chain of Ants looping and swerving around the tabletop (with some interesting side effects when the Leader crashes into its own tail).

I want to create a desktop version of the Ants. It'd be a slightly different look, though; Sprites instead of Ants. Remember that cool old screen saver I had on my Mac called The Swarm (where a bunch of streams of light followed their Queen around the screen)? Each Sprite would look something like that; a bright head with a pixel thin tail streaming out behind it and fading. The visual result would be The Swarm, only prettier, and certainly more interesting to watch.

As far as the mechanics, I want to reproduce everything the Ants can do and more. Each Sprite could have its own (user-designed) mathematical formula assigned to its movement, could be told to chase a particular Sprite or any Sprite, could be told to run away from a particular Sprite or all Sprites, seek out "food" nuggets, or perhaps a combination of all the above. With minimal programming effort on our parts, we could see extremely complex behavior arise. (I can't wait to put this thing out on the Net and see what users come up with...)

And best of all, it's a fantastic allegory for the RPG, but much simpler. No collision detection to worry about, no HP or armor or gravity or ground or anything like that. Just lots and lots of class interaction. I have reason to hope we'll come back to the main project with a renewed sense of direction. So what do you say? Are you willing to make a brief detour?
</blockquote>
