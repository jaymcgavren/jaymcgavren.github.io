---
layout: post
title: 'Custom MacOS App Keyboard Shortcuts'
tags: []
type: post
published: true
---

MacOS allows you to set custom keyboard shortcuts that activate any item in the menus at the top of the screen. You can do the same in Windows, but only with third party software; MacOS has this ability out of the box. This post has suggestions for things to add (and a couple default items to disable).

<!--more-->

Because these menus usually vary by app, you can set shortcuts that apply only when a specific app has the focus. That way the same key can be used for different menus in different apps. There's also an "All Applications" section for the few menus that appear in all apps.

To find the per-app shortcuts:

- Open System Settings.
- Click the "Keyboard" preference pane in the left-hand sidebar.
- Click the "Keyboard Shortcuts..." button, about halfway down the pane.
- A new modal will open.
- Click "App Shortcuts" in the sidebar of this modal.

Click the `+` button to add or change keyboard shortcuts for menu items in various apps. You choose the application you want to modify (or "All Applications" for a global shortcut), type the _exact_ name of the menu item you want to invoke, and press the key combination that should invoke it.

Some suggestions for items to add/change are below, broken up by app.

## All Applications

* "Show Help menu": Leave it activated and at its default of `Cmd-Shift-/` (a.k.a. `Cmd-?`). Incredibly powerful, because the menu opens with the "Search" box focused. This gives you a Spotlight-like search of the menus in every application, and lets you activate even menu items that have no keyboard shortcut without using the mouse. (Give it a try; I promise you'll be hooked!)
* "Minimize": Seems like this is redundant with the entry in the "Windows" section?! Remap it to something out-of-the-way like `Ctrl-Opt-Shift-Cmd-m` so that it's effectively disabled.

## Google Chrome

* "Select Next Tab": `Cmd-2` (This will override the shortcut to select the second open tab.)
* "Select Previous Tab": `Cmd-1` (This will override the shortcut to select the first open tab.)
* "New Window": It's `Cmd-n` by default but remap it to something out-of-the-way like `Ctrl-Opt-Shift-Cmd-N`. Why? Because you want the `Cmd-n` binding for something more powerful...
* "Move Tab to New Window": map this to the newly-available `Cmd-n`. This will take whatever the current tab is and, well, move it to a new window. Type `Cmd-t`, `Cmd-n` and you have the same functionality as the old `Cmd-n`. It takes a little getting used to, but I find this setup far more versatile.
* "Bookmark This Tab...": It's `Cmd-d` by default but remap it to something out-of-the-way like `Ctrl-Opt-Shift-Cmd-F6`. Why? Because you want the `Cmd-d` binding for something more powerful...
* "Duplicate Tab": map this to the newly-available `Cmd-d`. Why? Because duplicating the current tab lets you be at two places at once within a long page. Filling out a form but need to look at something else on the page? Just duplicate the tab, find what you need, and close the duplicate. You'll be back at the form you were filling out without losing your place!

## iTerm

* "Reset": Destructive and too easy to hit the default binding accidentally. Remap it to something out of the way, like "Ctrl-Opt-Cmd-F6".
* "Split Horizontally with Current Profile": You should be using a cross-platform solution like Tmux for functionality like this, and anyway it's too easy to hit the default binding accidentally. Remap it to something out of the way.
* "Split Vertically with Current Profile": Remap it to something out of the way.

## Keynote

* "Previous Slide": `Cmd-Shift-[`
* "Next Slide": `Cmd-Shift-]`
