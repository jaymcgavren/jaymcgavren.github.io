---
layout: post
title: 'Notes from Kernighan and Pike: The Practice of Programming...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1002'
  original_post_id: '1187'
  _wp_old_slug: '1187'
---
Borrowed The Practice of Programming from the Gangplank library on <a href="http://iamruinous.com/">Jade Meskill's</a> recommendation...  It's pretty C++ and Java-centric, but a lot of it is applicable to Ruby, and these notes were taken through Ruby-colored glasses.

<pre>
Style:

Why 'waste time' on good coding style?  Once it becomes automatic, even code
you produce under pressure will be better.
Using long names regardless of context is a mistake: clarity is often achieved
through brevity.
"queue.queue_capacity" is redundant, "queue.capacity" is better.
The ?: operator is fine for short expressions where it can replace four lines
of if-else with one, but if full conditional statements make the code clearer,
use those.
If you work on a program you didn't write, preserve the style you find there.
The program's consistency is more important than your personal preference.
Learn your language's idioms.  Those with experience can read and write them
easily without mistakes.  And if there's a mistake in using the idiom, it's
usually easy to spot.
Sprawling code goes onto multiple pages/screens; scrolling reduces readability.
If there's no good logic to put as the default in case statements and if-elses,
throw an exception; it catches conditions that "can't happen".
On comments:
        Harmful comments:
                Don't restate what the code already clearly says.  (Carefully
                chosen names are better than comments.)
                Don't write comments unless you're sure they will be updated as
                the code changes.
        Good comments:
                Aid understanding of a program by briefly pointing out
                important details.
        A comment that introduces each function will speed comprehension when
        reading code.
        If the code uses an unfamiliar algorithm, consider referencing a
        document/URL/book the maintainer can read.
        Comment anything unusual or potentially confusing, but only after
        considering refactoring.


Design and Implementation:

"Show me your tables, and I won't usually need your flowcharts; they'll be
obvious." --Frederick P. Brooks, Jr., The Mythical Man-Month
Program design can be colored by the language used, but is usually not
dominated by it.
Issues to be worked out in a design:
        Interfaces: provide services that are uniform and convenient, without
        so much functionality as to be unwieldy.
        Information hiding: provide straightforward access to your components.
        Hide details of your implementation so they can be changed without
        affecting users.
        Resource management: is the user responsible for managing storage,
        memory, and other limited resources, or is the framework?
        Error handling: who detects errors, who reports them, and how?  What
        recovery is attempted?
Build a prototype for new systems.  It's not until you've built and used a
version of a program that you understand the issues well enough to get the
design right.

</pre>
