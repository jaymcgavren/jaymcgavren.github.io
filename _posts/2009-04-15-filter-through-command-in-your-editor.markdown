---
layout: post
title: “Filter Through Command” in your editor...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1003'
  original_post_id: '1189'
  _wp_old_slug: '1189'
---
It's SO nice to finally have an editor (TextMate) with a proper "filter selection through command..." command.  I'll never go back to an IDE without one.

For those not familiar, commands like this take the current selection and pipe it through a Unix command (shell scripts, Perl, Ruby, Python, etc. included), then replace the selection with the command's output.  So if you have this text in the open document:

<pre>
foo
bar
baz
</pre>

You can select it, choose Filter Through Command (Cmd-Option-R in Textmate), type "sort" (the Unix command) in the dialog that appears, and wind up with this:

<pre>
bar
baz
foo
</pre>

<!--more-->

At work this ability has already replaced my need for a calculator; If I need the number of seconds in 24 hours, I type "print 60 * 60 * 24", highlight it, and pipe it to Ruby, and the result (86400) is sitting there in the open document (which is often where I need to use it, anyway).

Ruby's -n (loop through each line of STDIN, placing it in $_) and -e (evaluate the command line argument as Ruby code) are handy here, too.  I was viewing a Campfire (web chat) lobby page, and wanted the URLs for each chat room for making shortcuts.  So I viewed the page source and copy-pasted it into TextMate.  A glance determined that each URL was in the format "https://integrum.campfirenow.com/room/99999", where "99999" was any integer.  So I started filtering the document through commands.  It actually took a couple attempts to refine, but getting the original text back each time was a single Undo command away.  I wound up with this:

<pre>
ruby -ne "$_.scan(%r{https://integrum.campfirenow.com/room/d+}).each{|m| puts m}"
</pre>

$_ contains the current line, scan() gathers an array of matches for a regex, and the each() block prints each of them.  Note the backslash before the $; this keeps it from being interpolated by the "shell".

Out of the huge page of messy HTML, I was left with this:

<pre>
https://integrum.campfirenow.com/room/99991
https://integrum.campfirenow.com/room/99992
https://integrum.campfirenow.com/room/99993
...
</pre>

Much more manageable.

Of course, this is just one example; you can perform any operation against $_ that you can imagine.  Or you can leave off the -n argument to Ruby and work with $stdin directly, or even skip working with the input altogether and just replace it.

Voila - your text editor can do <em>everything</em> Ruby can do.  (Or Perl, or insert-your-favorite-language here.)  I'd be curious to see what tricks people come up with.
