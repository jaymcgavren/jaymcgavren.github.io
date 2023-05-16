---
layout: post
title: 'The Legend of Zelda: Tears of the Kingdom - Game Design Notes'
tags: ['game design']
type: post
published: true
---

Time for another post in my game design analysis series! This time I'm looking at The Legend of Zelda: Tears of the Kingdom.

Much of what I record here will be obvious to anyone who's recently played the game, or its predecessor Breath of the Wild. But I'm writing this for future readers as well, and hopefully it can provide some inspiration for a busy designers who don't have time to sit down and play the game themselves.

NOTE: Until such time as this note is removed, this post should be considered a work in progress. (I don't feel like messing around with a "draft" status and hopefully I can get some preliminary feedback this way.)

SPOILER ALERT: I am going to be making no effort whatsoever to avoid spoilers in these notes, as that would hamper their usefulness. If you don't want spoilers, play the game in its entirety before reading these notes!


<!--more-->


## Combat

Much ado has been made about this series's new weapon durability mechanic. To quickly recap here, some players hate it. But I personally buy into the argument that it's essential. If the first sword you found were durable enough to finish the game with, there'd be no point to looking for additional swords (and no need to explore).

New in Tears of the Kingdom: When you draw a weapon that is on the verge of breaking, a (non-modal) dialog pops up reminding you of this fact. This seems like a good idea, as the state of your weapons is potentially non-obvious otherwise.

Flurry Rush: bullet time something something drama. TODO: I know this feels good, but how DOES this work?

## Gameplay

Moonrise works just the same as in Horizon: Forbidden West. Immediately after sunset there is a period of considerable darkness, to the point that it hampers visibility a bit. _Then_ the moon rises, and it's nearly as bright as day again (but with different hues). Not sure if there's a gameplay purpose to this?

First cooking pot is positioned right near the entrance to the first Cold area. Spicy Peppers (which stave off Cold) are positioned near the pot.

Initial visit to a cooking pot displays a modal: "You can pass time by the fire." AFAIK this modal never appears again. Subsequent visits go straight to the modal: "Sit by the fire until: Morning. / Noon. / Night. / Never mind." Now, why ARE we allowed to pass time? Personally, I think the annoyance of walking around in the dark is reason enough, but are there other reasons? Why is there a day/night cycle at all?

Treasure chest, visible on a just-barely unreachable platform. I'm sure finding the item/ability that lets me reach it will feel rewarding.

Extremely Cold water and unclimbable icy cliffs used as impassable obstacles on path to first shrine.

Ukouh shrine: there's a moat that you're unlikely to fall into, but you need a way to climb out in the event that happens. A ladder was placed ascending out of the moat, but it's positioned such that a player won't see it unless/until they fall into the moat. So you see the ladder when you need it, but aren't distracted by it when you don't.

Levitating platforms cannot be grabbed from below and pulled down. It does seem like using a pair of them might allow a player to scale to any height (albeit in a very tedious way). So this probably keeps them from imbalancing the game even further.

There are significant differences in the effective ranges of the different abilities, e.g. Ultrahand requires you to be quite close, whereas Rewind can be used at range. Designers probably simply offered the maximum range for each ability that wouldn't imbalance the game (thereby maximizing the number of contexts in which each can be used), but it's interesting that they saw no need to keep the range consistent between abilities.

If the copious weapons from Breath of the Wild were still available, you'd have no need to use the Fuse ability. So the weapons are explained away by saying they were eaten by miasma during the Upheaval. It's super dumb but the player base seems accepting of it.

Dishes made with double the ingredients exactly double their replenishment/duration effects. Dishes made with discoverable, repeatable combinations of ingredients can be significantly more effective than their individual components.

Dishes sell for more than their raw ingredients. Dishes made with twice as many ingredients sell for (a bit) more than twice as much.


## Exploration

Temple of Time entrance: I rolled my eyes in annoyance when I marched all the way over to the Temple, only to be told I must first visit several shrines to gain entrance. But consider how awkward it would have been to be told "okay, go visit these shrines, and that will open the door on this temple you haven't been to yet."

How do you present the player with a couple interesting objectives at any given time, without overwhelming them? This YouTube [video](https://youtu.be/CZzcVs8tNfE) is actually about Breath of the Wild, but I'm sure these insights were re-used for Tears of the Kingdom.

Learning to use the Recall ability: you are presented with Recall when you are at a dead end in the Temple of Time. There's a risk players will turn around and leave again, so it's made very clear to you beforehand that this place holds a mainline quest and that now is the time to be pursuing it. With all this in mind, players will be intently looking around the room figuring out how to proceed, _and_ they have this shiny new ability they're eager to use. May as well try it on those giant spindles!

Then you're tasked with finding another shrine, whose location is marked on your map. The puzzle you're presented with requires two abilities. I personally actually forgot about the Ascend ability, and unable to scale the nearby wall, I started descending waterfalls. But it was soon very clear following that route would make it impossible to reach the marked destination. So, now that it was clear I was staring at a dead end again, I went back to the room and this time looked through my abilities again. I spotted Ascend there, and realized it would get me into position to use Recall. Puzzle solved thanks to subtle guidance from the designers.

Placing a character on the ground straining to look up indicates you need to surmount a wall to find Hoz.

## UI

When you first start out, there are two tabs in the `-` button menu marked "Feature not yet available". An alternative might have been to simply conceal the existence of these tabs. But there are benefits to revealing their existence:

- Keep the number of times needed to press `L` and `R` to get from one tab to another consistent, aiding habituation.
- Prevent players from forming a mistaken opinion that the game's feature set is quite limited.
- Pique player curiosity as to what these features might be, making unlocking them rewarding.

First time stamina wheel runs out: non-modal dialog saying something to the effect of "When your stamina wheel runs out, you'll be too tired to do certain actions until it fills again." Doesn't appear again on subsequent exhaustion; unsure if it ever does.

## Worldbuilding

There are clouds blowing by. Over the land. Because the land is in the sky, right? I love this because it's a reminder of your elevation and it's also _really fucking cool_.
