---
layout: post
title: 'Game Design Analysis - Roadwarden'
tags: []
type: post
published: true
---

Hopefully you've seen my game design [analysis of Subnautica: Below Zero](https://jay.mcgavren.com/2022/09/14/subnautica-below-zero-game-design-analysis.html). Here's another, for Roadwarden. It's an important game to me, as I hope to publish a text adventure myself at some point.

I wrote this while playing, and some of it reflects the mechanics I _hoped_ the game had, rather than what it actually _has_. No disparagement is intended; this is a rock-solid game and its author's choices were likely necessary and correct, grounded in reality rather than my fantasy of the perfect game.


<!--more-->



### Screen layout

Roadwarden is a "graphical text adventure". PC/Mac only, the author says a mobile port looks difficult or impossible.

The game _could_ have worked as text-only, but the simple graphics definitely help with visualizing map layouts, points of interest within a scene, etc.

### Attributes

Roadwarden starts out tracking just 4 attributes, with very coarse levels:

- Health: 4 levels
- Nourishment: 4 levels
- Armor: 4 levels
- Appearance (affects charisma): 5 levels

When you sleep, the quality of your lodgings (tent, inn, etc.) influences the amount gained or lost in these attributes.


### Tutorial

"Burning the dead [lest they reawaken] is not just a religious practice, it's a necessity... Making a large pyre takes a lot of time, but it saves lives."

Looks like subtle training in the game's tradeoffs. Your time is limited, but so is the peninsula's population.


### Special classes and dialogue choices

Taking a Scholar specialty opened a new option (craft gunpowder) when encountering a pack of griffons. It was represented simply, as a new dialogue path.


### Imagery

"You head toward the inn, hearing the piercing scream of a boar from the other side of the yard." Vivid imagery and world-building at the same time; if an inn in the wasteland wants to serve meat it must keep livestock. What did the authors draw on for inspiration? _Maybe_ certain movies or books, but a visit to a farm (and so many other locales!) would have been better.


### Adding difficult choices to conversations

Dialogue option: I could eat something. "Do you have any leftovers?"

I don't think the game has limits on NPC patience in conversations. If it did, it would be an interesting choice to "spend" some of that patience (and maybe some coin) in return for staving off hunger.

[Edit: I did finally find _one_ NPC with limited "patience". Most just let you pick off all the dialogue options, one by one.]

Many conversations include options that seem useless and even callous to the NPC. I have yet to choose one, but I wonder if they are traps, tests that the player is paying attention and being sympathetic.


### Maintaining context

Roadwarden has two different texts to refer to, which may inform your in-game decisions:

An "Archive", which is just like what I was already planning to provide in my own text adventure. It's a simple text log of events and dialogue that have appeared onscreen, that you can scroll back through. Not long, though, barely long enough to track all the events of a single village. And under a separate menu item from current dialogue.

And a "Journal", where your character records people, places, and other local knowledge he has learned on this journey. Additionally, the journal starts with entries on various universal knowledge the character would have had prior to beginning the journey. The journal entries are brief, basic, and omit some details covered in the actual dialogue (even ones that might improve minor decisions).

A journal entry starts out with a basic description, but may include the text "there's still more to learn about [it/them]", implying the main character will fill in details learned through experience or dialogue.

Multiple reviewers (including a publication) have expressed that they took their own notes, and did not object to doing so.


### Staying oriented

If you've already been to an area, that is subtly indicated within the text for the option to visit it: "I _return_ to the signpost" as opposed to "I _approach_ the signpost".

Players can access the map, journal, etc. at any time, even mid-conversation, which is important because you may need to refer to them.


### Time pressure

Thought has been given to what costs time and what doesn't. Travelling between areas within a town seems to be "instantaneous" (free). So do many simple dialogue options with NPCs. Longer roads cost time.

Time is valuable because you only have 40 in-game days to work with. And you don't want to be caught on the road at night; you'll be attacked by monsters and are guaranteed to lose health.




### Imperfections

There are certain continuity errors, such as your character suddenly knowing the name of Caius without anyone mentioning it. PCGamer noticed these in [their review](https://www.pcgamer.com/roadwarden-feels-just-like-cracking-open-a-huge-fantasy-novel/), but most Steam reviewers did not.



### Writing

Unique, colloquial language.

One functional invention is the universal substitution of "shell"/"shells" for body/bodies (a word frequently used in creature descriptions). Saves a whole syllable!


### Puzzles

Every NPC you meet puts up a front of honesty and competency. (As a real person might for their neighbors.) For some NPCs this is just a front, and it's up to you to figure out which.


### Technical/Business aspects

* Game was released in September 2022.
* As of February 2023 it has 1,309 Steam Reviews.
* Assuming [review:sales ratio of 1:63](https://newsletter.gamediscover.co/p/how-that-game-sold-on-steam-using), that's about 80,000 units sold.
* Regular Steam price is $11, has never been on sale below $8.25.
* That means revenue in the ballpark of $800,000.

All code, writing, _and art_ on Roadwarden appears to have been done by one man, [Aureus](https://twitter.com/MoralAnxiety). (I assume music was contracted.) He's based out of Wrocław, Poland. There is an "editor" in the credits, who I'm sure helped _a lot_ with producing the polished final text.

This is Aureus's most successful game, but was not his first; he has at least two others set in the same world.

Engine, evidently, is Ren'Py, which is built on top of Python and SDL. Considering the stack, I would have expected the creator to have more trouble packaging and distributing the finished product, but everything installed and ran flawlessly, even on my Mac. It does seem to rule out a mobile port, though.

Game is available on Steam and GOG.
