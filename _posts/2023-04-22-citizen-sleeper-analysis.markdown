---
layout: post
title: 'Game Design Analysis - Citizen Sleeper'
tags: ['game design']
type: post
published: true
---

Time for another post in my game design analysis series! This time I'm looking at Citizen Sleeper, an indie work of interactive fiction released in 2022 to much critical acclaim and "overwhelmingly positive" Steam [reviews](https://store.steampowered.com/app/1578650/Citizen_Sleeper/).

An uncharitable review of Citizen Sleeper would call it a "choose your own adventure"-style game, where all your options are chosen from a menu, and the game reacts accordingly. And indeed, it seems like the actual coding implementation is probably about that simple. But the design surrounding that is extremely impressive.

I bet it was possible to prototype this game entirely on paper (regardless of whether they actually did so), thus front-loading much of the project risk. It could have been determined whether the game was fun to play (and therefore more likely to succeed) before hiring a single developer or even any writers. That seems like a model worth emulating.


<!--more-->


## Gameplay

The game takes place on a circular space station, which keeps all the locations one needs to travel between in a straight line, which means moving on the map is a simple matter of scrolling the mouse wheel. It's an incredibly efficient interface. In fact, maybe a little _too_ efficient; in a couple places the developers add "ferrys" one has to click through just to add a little friction.

You roll dice each day (from one to five dice depending on your condition), and you choose which actions you'll apply your high rolls to (more likely to succeed), and which actions get your low rolls (more likely to fail). Thus simultaneously introducing elements of both chance and strategy.

Some locations make you wait a certain number of days between actions, introducing a need for multitasking.

In the early game, "safe" actions with minimal negative consequences are provided as sinks for one's low dice.

The game also lets players switch into a Matrix-like cyberspace reality. Many actions here _require_ low dice, acting as an additional sink for them. But there is no visual reminder of cyberspace targets in the "real world". So there are still moments of "what will I do with these 1s and 2s that I rolled?" until the player remembers to switch into cyberspace.

Cyberspace is formed as a shadow of the "real world", allowing for interesting confluences between the two, though I feel this was not used to its full potential.

The "Instant Karma" perk takes a while to earn, but it's literally a game changer, letting you re-roll all your remaining dice once each day. So you spend the high dice, re-roll, and hope the low ones turn to high ones. The late game probably had to be re-balanced for this mechanic but it's quite fun.

Later "episodes" in the game cut off the original means by which you acquire "stabilizer", an essential resource like food or water. They then provide a new source of stabilizer acquired by different means. If the old rules for getting stabilizer were somehow incompatible with the rules of the new episode ("broken", overpowered, underpowered), this would have allowed the developers to switch to new, compatible rules.

[Citizen Sleeper](https://www.fellowtraveller.games/citizen-sleeper) is available on PC, Mac, Switch, and XBox (included with Game Pass as of April 2023).
