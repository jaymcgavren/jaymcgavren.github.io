---
layout: post
title: 'Coping with MacOS Mojave for Web Development'
tags: []
type: post
published: false
---

For pretty much every Mac I've ever owned, I've copied my configuration from machine to machine. But when you do so, a lot of unused cruft builds up over the years. So I've decided to wipe everything and start totally (well, okay, mostly) from scratch. This is a rare learning opportunity and so I'm documenting my setup here, for my reference and for yours.

This post is intended to be a living document. I'll be updating it as I discover improved settings. Comments and suggestions are welcome!

Be warned: the tone is cantankerous. I don't like the direction recent MacOS versions have gone, and many of my settings are an attempt to get back to "the good old days". If you're one of those fans who think Apple can do no wrong, and you want to make use of all the latest MacOS features, you may want to find another configuration guide. Now get off my lawn!

<!--more-->

First, we need to kick off a bootstrapping script to install common tools you'll need. This is going to take a long time to run so it's best to get it going now.

* My employer uses a fork of Thoughtbot's [Laptop](https://github.com/thoughtbot/laptop) script. Your employer may have their own.
* I wrote [my own provision_osx_computer.rb Ruby script](https://github.com/jaymcgavren/dotfiles/blob/master/osx/provision_osx_computer.rb) a while back but it's a bit outdated. You might consider forking it and using it as a basis, though.

Next, let's visit "System Settings" to fix some terrible defaults:

* "Desktop & Screen Saver"
    * Theme: "Dark (Still)". Might help you fall asleep after a late night hacking session.
* "Trackpad"
    * "Point & Click" page
        * Look up & data detectors: Disable. I don't want my trackpad doing random useless stuff because I clicked "too hard".
        * Secondary click: Disable. I don't want my trackpad doing random stuff because I didn't lift a finger.
        * Tap to click: Disabled by default and needs to stay that way. Why is this crap even a setting?!
        * Force Click and haptic feedback: Disable.
    * "Scroll & Zoom" page
        * Scroll direction: Natural: Disable. I learned the old way and I'm not switching until I have no choice.
        * Other settings: I'm leaving these at the default (enabled), until such time as they piss me off.
    * "More Gestures" page
        * Disable all this crap! Mission Control, Exposé, Launchpad, all of it. Here's why:
            * These features only exist on MacOS (at least in this exact form). Get too used to them and you won't be willing/able to switch to another OS when the time comes.
            * These gestures can be invoked accidentally.
            * They're only there for damn dirty mouse/trackpad users. Ain't nobody got time for that. _You_ use your keyboard and a window manager.
* "Dock"
    * The dock is for damn dirty mouse/trackpad users, not for you. I don't think it can be disabled entirely with stock software (please let me know if I'm wrong) but you can minimize how much it gets in the way.
    * Size: minimum
    * Magnification: disable
    * Position on screen: Leave at default of "Bottom".
    * Double click a window's title bar to: Disable this. You should be using a window management program to minimize/maximize windows.
    * Automatically hide and show the Dock: Enable so that at least it's hidden most of the time.
* "Keyboard"
    * "Keyboard" page
        * Key Repeat rate: Max it out.
        * Touch Bar shows: I've never used the Touch Bar and I refuse to start. Change it to show "F1, F2, etc." This also gets your Esc "key" back. The whole setup still sucks because there's no tactile key press, but at least now it won't randomly change functions on you.
        * Unless you enjoy SHOUTING when typing often, the Caps Lock key is worse than useless - it's a booby trap sitting in the middle of your keyboard. Click the "Modifier Keys..." button, and remap Caps Lock to Control.
    * "Text" page
        * For God's sake, uncheck everything here! Why on earth do they have it messing with your text as you type by default?!
        * Be sure to click the "-" button to remove any text expansions, too.
    * "Shortcuts" page
        * Full Keyboard Access: Set to "All controls".
* "Sharing"
    * Computer Name: This includes your user name by default, which is info I'd rather not leak to the network. Rename it to [something cool](https://en.wikipedia.org/wiki/Lists_of_deities)!

Hope you found this post helpful (and not _too_ offensive)! I'm open to healthy debate about the merits of these settings. Who knows, you _might_ even change my mind about something. Leave a comment below!
