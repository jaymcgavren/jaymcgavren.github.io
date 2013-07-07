---
layout: post
title: 'Notes from RailsConf - Starting Up Fast: Lessons from the Rails Rumble...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1013'
  original_post_id: '1203'
  _wp_old_slug: '1203'
---
Hosted by Nick Plante (Nth Interactive)

Would've liked to give attributions for these quotes, but it wasn't practical.  Sorry!

<pre>
Rails Rumble:
        48 hours to design, develop, and deploy a micro-app.
        Public voting.
Panel:
        Joe Fiorini
                Grand prize winner, 2008
                meetbetween.us
                Team of 4
        Ben Scofield
                Solo Division, 2007, 2008
                Forever Home (down)
        Chris Saylor
                Grand prize winner, 2007
                tastyplanner.com
                Team of 4
        James Golick
                Most Useful, 2008
                "What Does This Error Mean?" site
"How is the Rumble like working on a normal Web project?  How does it differ?"
        Time constraint means you won't be building a social network, etc.
        What can you cut out?  Do you need a login system, for example?
        People likely to visit site, make snap judgement on first page, and
        leave again.
"Is it possible to build a real product this way?  Have you continued to
develop your entry apps?"
        Real Simple Magazine did a couple hacknights later.  Someone contacted
        them to acquire it later.
        Joe got approached by yellowpages.com, though nothing has materialized
        yet.
        No matter how great your initial idea is, you don't REALLY know what
        you want to build until you start.
                Getting app active and getting feedback is great.
"What sort of up-front planning and design work did you do?"
        Complete wireframe on pen and paper (digital wireframes not allowed),
        assignment of tasks to developers.
        "None."
        5 or 10 stories in Pivotal, not much.
        Color selection, finding stock photos.
"How much time did you spend in prep, and does that affect the spirit of the
Rumble?"
        You can plan as much as you want if you're not creating digital assets.
         Much of this is on the honor system.
        "We didn't want to spend 48 hours thinking, [so we planned up front]."
        Moderator: We want to encourage use of the sea of third-party plugins
        that are out there.
        "We got shit marks for design, probably because we didn't do any."
"How did you plan for the 80/20 rule?  (20% of small tasks take 80% of the
time.)"
        We ensured that even if there were small tasks we hadn't completed, we
        could still deploy.
        Ben Scofield expounds: Version he was working on at deadline had a bug,
        but version control let him back out to a stable version.
        We talked about features we wanted up front.  Got a backlog going.  Our
        mantra: "Think of Google".  Try to have nothing but a search box and a
        couple buttons.
        A 48-hour competition is a terrible place to mentor someone.  Make sure
        you know all the
"Did you use automated testing when you built your application?"
        No.  TDD can make you faster for big apps, but it slows you down on
        small ones.
        Yes, some.
        Yes.  Automated tests are great for catching regression.  It's just a
        good development practice.
        Testing is a method of design.  If I need to get something done quickly
        and can't test, I do 'design by wishful thinking'.
                Write the code the way you want to see it, then go implement
                it.  [Sounds like comment-driven development to me.]
        Don't let them fool you.  You can still win if you don't do testing.
"What plugins/gems/tools did you find most helpful?"
        Plugin by James Golick helped build RESTful contollers without need to
        code.
        Starter apps - Bort, Blank.
        Moderator: Rails 2.3 Templates offer starter-app-like functionality.
        Factory Girl, Shoulda, Mocha.  Make Resourceful.
        New Relic RPM - it helped us at one point when LifeHacker post
        generated 2000 hits during voting period.  MySQL fried, not Rails, and
        RPM helped spot that.
        Almost everyone used Campfire.  Inline paste, inline images, chat
        history are nice.
        Basecamp.
        Pivotal Tracker.  Super-lightweight tool to keep organized without
        eating our time.
"How did you find other people to work with and decide that you could work with
them?  Is it anything like finding co-founders for a startup?"
        Talked to good friends first.  At last minute, had to call every local
        Rails developer we knew to replace a dropout.  Worked out well.
        Find a well-rounded team.  Sysadmin, DB design, graphic design,
        developer.
        Good friends from local developer community.  Wound up hiring two of
        them.
        Local user groups.  Refresh to find designers.  Ruby User Groups for
        developers.
"What was the most rewarding part?"
        Getting to work with awesome people.  Did screencast too.  It was a lot
        of fun.
        Getting to know people better.  Getting to release a completed app- so
        often, real life interferes with completing a project; not here.
        You get so bogged down working on large apps for an employer.  This
        reminds you what's great about coding.
        Moderator: "Launching shit is awesome."
"How much sleep did you get?"
        4 each.
        6 each.
        4-6 each.  One member went to concert, but coded in car on way there
        and way back.
        6 hours per night.
        You don't have to work 44 of the 48 hours, just set realistic
        expectations.
</pre>
