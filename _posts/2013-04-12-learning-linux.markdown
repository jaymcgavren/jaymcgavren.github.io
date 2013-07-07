---
layout: post
title: Linux - What to Learn First
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1130'
  original_post_id: '1504'
  _wp_old_slug: '1504'
---
Originally wrote this as a Facebook post to guide my brother, who's been stuck in Windows-land for a long time and needs to learn some Linux for work...




I dunno <em>why</em> there still isn't a single definitive reference I can point someone to...  Too big a topic, I guess.


<h2>Step 1</h2>

Acquire a good reference.  Ask around at the office - everyone will have a favorite book.  Here's a decent one I've used: <a href="http://www.amazon.com/Unix-Nutshell-Fourth-Arnold-Robbins/dp/0596100299">Unix in a Nutshell - Fourth Edition</a>.  (Cheap older edition <a href="http://www.amazon.com/Unix-nutshell-Third-Arnold-Robbins/dp/B001RG1QU4/">here</a>.)


<h2>Step 2</h2>

Learn to ignore elitists who tell you you're going to shoot your eye out.  You <em>don't</em> need to know everything - wait until you get stuck, and then Google the error messages you get.  (In the bad old days you <em>used</em> to be able to erase your whole file system, but nowadays ordinary users aren't given the kind of system permissions that would let them do that kind of harm.)


<h2>Step 3</h2>

Learn some commands.  I spend the most time with these:

<em>SSH</em>: Get to prompts on remote systems.  Learn this one inside and out, including passwordless login via public/private keys.

<em>man</em>: Bring up a manual page on any command.  Reading manpages is itself an art, so find a good tutorial on fully understanding manpages.

<em>bash</em>: Learn this shell; it's the most common.  It will change the way you work with files forever.  Learn how to pipe programs' standard input and output.  Learn how to redirect output to a file.

<em>ls</em>: List files and directories.  Learn this inside and out.

<em>find</em>: recursively search the whole hard drive for files and folders.

<em>xargs</em>: run commands on the files brought up by ls and find.

<em>chmod</em>: Control who can read, write, and execute (run) files.  This will cause you grief if you don't know it.

<em>scp</em>: Secure CoPy.  Transfer files.  Combines with SSH to do it passwordless-ly.

<em>rsync</em>: Even more powerful copying tool.  Again, combines with SSH.

<em>less</em>: Read text; something you'll need to do a lot.  man and other programs pipe output through less, so learning it is worthwhile.  Especially learn its string search capabilities.

<em>vi</em>: If and only if you have to edit files while they're sitting on a remote server, learn vi.  It's a pain, it's counterintuitive, and you're going to be expected to know it.

<em>cron</em>: Schedule commands to be run at a particular time of day/week/month/year.  Look like you're working hard when you're not even at the office.


<h2>Step 4</h2>

Get a buddy.  Until you have some experience, you'll want someone to confer with on the best way to do things.  If a local buddy isn't available, get good at Googling and posting questions on forums like <a href="http://serverfault.com/">ServerFault</a>.


...all that's a bit much, I know.  If you learn only two of those, learn SSH and bash.  Any time spent learning these topics will pay dividends, even if all it does is save you time.
