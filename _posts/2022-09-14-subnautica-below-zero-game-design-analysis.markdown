---
layout: post
title: 'Subnautica Below Zero Game Design Analysis'
tags: []
type: post
published: true
---

Ever since I became serious about game development, I've been picking games I play apart as I go. Dissecting the controls, the menus, the progression gating. Subnautica: Below Zero is my latest obsession. Here's a catalog of things I noted as I played.

<!--more-->

## Core Gameplay

Tension is maintained by your ever-lowering stats, each of which is replenished by a different resource or action.

- Oxygen. Replenished by surfacing.
- Hunger. Replenished by food.
- Thirst. Replenished by water.
- Health. Inevitably decreases with exposure to aggressive creatures. Replenished by first aid kits.
- Inventory space. Consumed by food, water, and first aid kits.

You have a laundry list of maintenance that you'd be wise to remember before leaving your base. Most players won't consider this "fun" but I'd argue that remembering them all and learning to carry them out efficiently is satisfying.

- Restock food, water, first aid kits.
- Replace batteries in all equipment (a dedicated "swap battery" key speeds this up).
- Repair sea truck, all its modules, and the Prawn, and replace their power cells.

You "power up" as you progress by discovering more powerful equipment and sources of supplies.

- Avoids tedium by requiring restocks less frequently.
- Enables deeper exploration further from base.
- Frees up inventory space, since individual items have greater effect.

## Other Details

Base building, repairs, object scanning, and other activities require you to exit your vehicle, leaving you in a vulnerable position. (Tension!)

Scanner room lets you gather large quantities of items, but only one type at a time. Its directions are very vague until you make the HUD upgrade, at which point items are marked with transient beacons.

Prawn suit eliminates worries about oxygen and injury, with the tradeoff that you can't swim, only jump. Sea truck handles oxygen, safety, carry capacity, and item crafting, with the tradeoff that you can't fit into tight spaces.

You can hear leviathans from some distance away. The distinctive roars tell you what type of creature you're up against.

 Broken green cables lead you to alien installations from far away. If the facility was just a lone door in the landscape, stumbling on it would feel random and unsatisfying, and many players would never find it at all.

Charging swim fins eventually eliminate the need for swapping batteries in your tools.

There is a secondary power cell on the sea truck that remains at 100% charge until the first cell is fully depleted. This means there is usually only one cell to replace. It also reduces the likelihood of the truck being stranded.

## A Model

I've realized Subnautica and its sequel are a good model for the text adventure game I want to build. They have the exploration, crafting, and resource management elements that reliably get me hooked on a game. But more importantly (and uniquely), they de-emphasize violence and combat. I'd call them required playing for any would-be game designer.
