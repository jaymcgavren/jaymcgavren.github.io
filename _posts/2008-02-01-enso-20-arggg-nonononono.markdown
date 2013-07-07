---
layout: post
title: Enso 2.0 - Arggg nonononono!!!
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '713'
  original_post_id: '762'
  _wp_old_slug: '762'
---
Just saw <a href="http://humanized.com/weblog/2008/01/31/enso-20-design-thoughts">Aza Raskin's post to the Humanized Weblog regarding "Enso 2.0"</a>...

...and I hope I'm wrong, but I'm filled with a sense of impending doom.  The champions of amodality are turning to the Dark Side.

<blockquote>Enso shouldn't make you type all of "open" every time</blockquote>

Yes it should.  If a command is important enough to use repeatedly, the user will get very fast at typing it.  If it's so important, make the command short (and "open" is short enough).

<blockquote>Enso should gracefully handle the case where there's no convenient place to enter text</blockquote>

Give us enough commands that we never have to leave our editor, then.  (Remember The Humane Environment?  The Canon Cat?)  Don't introduce unneeded complexity into the Enso interface itself.

<!--more-->

<blockquote>Enso shouldn't require you to type out text, select it, and then run a command when you'd rather run the command and then enter the text (think calculate)</blockquote>

After enough uses, my thought process would be: "OK, '60 * 60 * 24 * 365'...  [highlight]  [command 'calculate']".  "Calculate" is, in my mind, the "turn this equation into the number I actually need" command.  I don't want to be typing "calculate" while trying to remember a complicated series of numbers and symbols.

<blockquote>You could even type the parts that were most memorable to you. For instance, "offox" would match to "open firefox", and "trantojap" would match to "translate to japanese ".</blockquote>

And yet in the same article, they complain about Unix "df" and "tar -xvzf".  Again, make them type it.  They'll type more, but they'll think less (and disrupt their actual task less).

<blockquote>it is cumbersome to type "translate to french outrageous accent", and impossible to type "calculate 4+(2+.5)^3/5? (shifted characters aren't type-able while holding down the command key).</blockquote>

Again, I'm thinking "'outrageous accent' in french", not "french outrageous accent".  The current system of highlighting and converting to the desired result is just fine.  And what if I need to translate something to French, German, and Japanese?

<blockquote>Novice users can type out the easy-to-learn-and-remember full command name ("open"). Long time users can just use one-keystroke commands ("o"). Thanks to our new learning algorithm (I'll come back to this in another section), those shortcuts will train themselves to your use patterns, yet never shift around on you. This means that the time cost for choosing a command is greatly reduced. Using Caps Lock "o" for open is key-wise equivalent to a hot key for calling up a dedicated launcher! Good design erases the line between beginners and experts.</blockquote>

And yet you're having experts type a completely different phrase than the beginners.  An "expert mode" that's the result of an adaptive algorithm is no better than one that's designed into the software.

<blockquote>Our argument is that the state of the system (e.g., that your keystrokes are going into the entry area and not into the application) will almost always be the user's locus of attention. The entry area will never appear unless the user actively asks for it, so they are never surprised, never enter the information in the wrong spot, and never make mode errors.</blockquote>

Note the "almost" in "almost always be the locus of attention".  The Humanized offices probably don't have children running around them, but my house does.  Distraction is always waiting to strike at the least convenient moment.  And when I return to the machine, I might not really start typing prose into that waiting calculate window, but I'm going to stop and think about whether it's open.  I came to Enso to get away from that sort of stuff!

<blockquote>So we added a "resume" command to the design. If you are trying to interact with something else on your system, then Enso fades away with a transparent message telling about the "resume" command. The resume command does exactly what it sounds like: it resumes the state of Enso exactly where you left it.</blockquote>

Doesn't help in the situation I just described - I haven't interacted with anything other than the keyboard.

<blockquote>you'll only use the resume command when you know exactly what's in there, i.e., that it is your locus of attention (even if it is invisible). How is this different than the invisible buffer that is copy and paste? Only in one important way: That resume is not being used for storing important content that might not exist elsewhere.</blockquote>

They're proposing typing entire e-mails into Enso.  I'd call that important content.

<blockquote>A lot of our readers have been arguing persuasively that we were too heavy-handed in dismissing all adaptive interfaces. If the algorithm respects habituation, then we have no right to complain.
...
Eventually, you'll want to be able to go to any computer and have Enso know who you are, so that all of your habits can be preserved (Weave, anyone?). But, that's for much later.</blockquote>

Why introduce this unneeded complexity?  A user's expertise and habits are stored in their own grey matter, and they carry <em>that</em> with them to every computer they use, networked or not.

Another post on the Humanized blog talks about the importance of software projects having a benevolent dictator...  It's time for Humanized to show their benevolence (and their authority).  Don't let the slow typists among your users ruin Enso for everybody.
