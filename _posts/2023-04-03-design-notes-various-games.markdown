---
layout: post
title: 'Design Notes on Various Games'
tags: ['game design']
type: post
published: true
---

Hopefully you've seen my [analysis of Subnautica: Below Zero](https://jay.mcgavren.com/2022/09/14/subnautica-below-zero-game-design-analysis.html). There are many other noteworthy puzzles, mechanics, and conventions in games, but most games don't warrant a blog post unto themselves. This post is a catch-all for other patterns I want to record.

This will be a living document, so expect edits and additions over time. (Yeah, that's not how blog posts are supposed to work. Send me some traffic and I'll start following the rules.)

<!--more-->

# General Gameplay

Power attacks do heavy damage, but have a windup and/or a recovery time, during which you are vulnerable.

Heavy objects can only be dragged along level, smooth surfaces, thus constraining them to a particular area (and keeping the player from wasting time and ruining other puzzles by dragging a box everywhere they go).

Enemies and breakable objects can serve as markers of where you _haven't_ been. If an area is littered with broken crates and devoid of enemies, it's an implicit sign that you've already explored there.

Weird West: You can carry raw meat on you, but it can only be prepared at a campfire, and must be consumed immediately. This restricts food consumption to the campfire, while still requiring that inventory space be spent to carry the meat.

When implemented well, "poisoned" status imposes an interesting set of constraints on normal gameplay. Historically, being poisoned just results in a choice between taking the damage or giving up one attack turn to take an antidote that you already have in an infinite-capacity inventory. Boring! More interesting, to me, is dropping what you're doing and rushing to find an NPC who can treat the character, all while they are taking damage or are otherwise de-buffed.

# UI

If objects need to be interacted with, they are glowing and flashing, or at least heavily lit. They are never static in appearance.

When a stat changes, animate the change to draw attention to the fact that it's changing as well as the amount of the change. E.g. red delta on the HP bar in Street Fighter, or energy decreases in Citizen Sleeper.

Weird West: When enemies switch to alerted status, a HUD message explains the reason e.g.: "A body you left behind was spotted". Avoids confusion over why they were alerted.

# Co-op Multiplayer

Deep Rock Galactic: Some enemy types (glyphid grunt guards, praetorians) have extra armor in the front, making them resistant to the player they are approaching. But they are weaker on the sides or rear, meaning a flanking player will do extra damage to them.

# Risk/Reward

Pipe Dream: The cross piece is versatile. If you're in a hurry (or inexperienced), it's just a piece that can complete a horizontal OR a vertical pipe. But it also allows taking a risk to earn points: forming a loop to route the sludge through both the horizontal and vertical portions of the pipe. Loop bonuses even multiply if you nest loops within loops. But trying to complete a loop greatly constrains the path your pipe can follow.

Yoshi: Not a great game overall, but an example of risk/reward: You want to stack tiles as high as you can atop a bottom-half egg shell, and hope you get a top-half before you run out of space. The more tiles compressed into an egg, the bigger the bonus.

Slay the Spire: "now vs. later" - adding items or abilities that are useful now but less-so later in the game, or that will be useful later but acquiring them is a drain on your (precious) resources or time now. You can risk death now to acquire this late-game item (resulting in a spectacular change of fortunes later), or get items now to help you survive, but risk being underpowered for the late game. From developer Casey Yano in [this podcast episode](https://eggplant.show/15-gdc-special-derek-yu-and-slay-the-spire).
