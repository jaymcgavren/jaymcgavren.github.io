---
layout: post
title: __pre_to_s, __post_to_s...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '842'
  original_post_id: '940'
  _wp_old_slug: '940'
---
The design by contract bits in the Ruby Cookbook are interesting if only for the fact that they got me thinking about all the options for wrapping a method.  By including a module in your class, you can set up code to run before or after a method call, for a specific method or all methods.  That means you can check arguments, check output, or maybe even alter the input or output.

When flipping through the Module documentation this time, my only thought was, "Oh, neat, they have #included, #extended, and #method_added callbacks.  Those might be useful someday."  Well, only now am I starting to see concrete uses, and they're potentially so powerful it blows my mind.

My main remaining gripe is how sloppy aliasing methods is.  I'd rather not have a bunch of __pre_x(), __post_x(), __original_x() methods lurking under the hood of my classes.  But at least it's becoming clear that I can hide this ugliness from myself.
