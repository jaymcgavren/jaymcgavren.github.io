---
layout: post
title: 'Coping with MacOS Sequoia for Web Development'
tags: []
type: post
published: true
---

<!-- TODO fix line gap between nested bulleted lists -->

This is the latest in a series of posts on using MacOS for web development. This fork of the original post is targeted at Sonoma (14.4).

For pretty much every Mac I've ever owned, I've copied my configuration from machine to machine. But when one does so, a lot of unused cruft builds up over the years. So I've decided to wipe everything and start totally (well, okay, mostly) from scratch. This is a rare learning opportunity and so I'm documenting my setup here, for my reference and for yours.

<!--more-->

This post is intended to be a living document. I'll be updating it as I discover improved settings. Comments and suggestions are welcome!

Be warned: I am an Apple skeptic. I don't like the direction recent MacOS versions have gone, and many of my settings represent an attempt to get back to "the good old days". If you're one of those fans who think Apple can do no wrong, and you want to make use of all the latest MacOS features, you may want to find another configuration guide. Now get off my lawn!

## Portable config with a dotfiles repo

You _can_ do a mass copy of your user's home directory from machine to machine, but that assumes you're not recovering from a hard drive crash or stolen laptop. Far better to create a version-controlled repo (I use Git) with the contents of the "dotfiles" (`.zshrc`, `.tmux.conf`, etc.) in your home directory. Here's my repo on GitHub:

[https://github.com/jaymcgavren/dotfiles](https://github.com/jaymcgavren/dotfiles)

To retrieve it I do something like this:

``` shell
cd ~
git clone git@github.com:jaymcgavren/dotfiles.git
```

The repo includes a README with directions on how to link its contents so they're used as your system config.

## Developer Command Line Tools

We need the XCode "command line tools" before we can do much of anything from the terminal. These will take a long time to download and install so it's best to get this going as soon as you can.

* Open `/Applications/Utilities/Terminal.app`.
* Type `git`.
* We're not actually using Git yet, but attempting to run it will pop up a GUI window prompting you to install the command line tools. Follow the prompts and they'll be downloaded and installed.

## Install packages

We need to kick off a bootstrapping script to install other common tools you'll need. This too will take a long time to run, and you probably can't kick it off until the XCode tools finish installing.

* My employer uses a fork of Thoughtbot's [Laptop](https://github.com/thoughtbot/laptop) script. Your employer may have their own.
* I wrote [my own provision_osx_computer.rb Ruby script](https://github.com/jaymcgavren/dotfiles/blob/master/osx/provision_osx_computer.rb) a while back. You might consider forking it and using it as a basis for your own.

After installing so many new programs, I'd recommend rebooting your machine, just in case.

## Fix Terminal.app

By default, MacOS Terminal.app doesn't treat the Option/Alt key as a Meta key. This breaks many shortcuts in `set -o emacs` mode (the default) as well as Emacs itself. Personally, I use iTerm 2 for my terminal, but we should fix Terminal.app regardless.

* Open `/Applications/Utilities/Terminal.app`.
* "Preferences..." menu.
* "Profiles" page.
* Cmd-a to select all profiles.
* "Keyboard" page.
* "Use Option as Meta key": enable.

## Window Manager

I avoid using the mouse as much as possible in my daily work. Sure, it's well-suited for drawing and such, but for common operations like switching between apps, it's unacceptably slow. MacOS supports some shortcuts like Cmd-Tab, but those are pretty limited.

That's why I use a "window manager" app. A window manager can remember the positions your windows are in, and restore those positions for you at the press of a hotkey.

You have a few good options that I know of:

* [Slate](https://github.com/fertigt/slate_arm64): This is what I use. Open-source, configured via [text file](https://github.com/jaymcgavren/dotfiles/blob/master/slate).
* [Moom](https://manytricks.com/moom/): Closed-source, $10 USD. Looks fancy, seems popular, haven't used it.
* [SizeUp](http://www.irradiatedsoftware.com/sizeup/): Closed-source, $13 USD. Seems adequate.


## Fix System Settings

Next, let's visit "System Settings" to fix some terrible defaults.

### "Appearance" Preference Pane

Appearance: "Dark". Might help you fall asleep after a late night hacking session.

### "Lock Screen" Preference Pane

"Require password after screen saver begins or display is turned off": "Immediately".

### "Trackpad" Preference Pane

#### "Point & Click" page

* Force Click and haptic feedback: Disable.
* Look up & data detectors: Disable. I don't want my trackpad doing random useless stuff because I clicked "too hard".
* Secondary click: Disable. I don't want my trackpad doing random stuff because I didn't lift a finger.
* Tap to click: Disabled by default and needs to stay that way. Why is this crap even a setting?!

#### "Scroll & Zoom" page

* Scroll direction: Natural: Disable. Enabling it seems fine on a trackpad but since at least Mojave it reverses a mouse scroll wheel too, which is not fine.
* Other settings: I'm leaving these at the default (enabled), until such time as they piss me off.

#### "More Gestures" page

Disable all this crap! Mission Control, Exposé, Launchpad, all of it. Here's why:

* These features only exist on MacOS (at least in this exact form). Get too used to them and you won't be willing/able to switch to another OS when the time comes.
* These gestures can be invoked accidentally.
* They're only there for damn dirty mouse/trackpad users. _You_ don't have time for that; you use your keyboard and a window manager.

### "Desktop & Dock" Preference Pane

#### Dock section

The dock is for damn dirty mouse/trackpad users, not for you. I don't think it can be disabled entirely with stock software (please let me know if I'm wrong) but you can minimize how much it gets in the way.

* Size: minimum
* Magnification: disable
* Position on screen: Leave at default of "Bottom".
* Double click a window's title bar to: Disable this. You should be using a window management program to minimize/maximize windows.
* Automatically hide and show the Dock: Enable so that at least it's hidden most of the time.

#### Desktop & Stage Manager section

I don't need to know what Stage Manager is to know I don't care about it; it's proprietary and therefore you don't want to be habituated to it. As best as I can tell, here's the most you can do to disable things; leave everything else at the defaults.

* "Show items on desktop": disable
* "Stage Manager": Leave it turned off.
* "Show recent apps in Stage Manager": disable

#### Widgets section

See "Desktop & Stage Manager"; turn it all off. Widget style can stay at "Automatic".

#### Windows section

More proprietary stuff you should avoid getting used to. Use your window manager for this kind of thing instead.

* "Prefer tabs when opening documents": "Never"
* "Drag windows to screen edges to tile": off.
* "Drag windows to menu bar to fill screen": off.
* "Hold option key while dragging windows to tile": off.
* "Tiled windows have margins": definitely off, even if you kept window tiling on.

#### "Mission Control" section

More proprietary stuff you should avoid getting used to. Use your window manager for this kind of thing instead.

I don't believe you can turn it off altogether, but you can disable everything in this section.

* Under "Keyboard and Mouse Shortcuts", disable all shortcuts:
    * Mission Control: select `-` from the dropdown.
    * Application windows: select `-` from the dropdown.
    * Show Desktop: leave at the default, blank. Or if that doesn't work, select `-`.

#### "Shortcuts..." button at the bottom

This displays the "Keyboard & Mouse Shortcuts" modal.

For "Mission Control", "Application windows", and "Show Desktop", disable both the keyboard shortcut and mouse shortcut. (Scroll to the bottom and find the "-" in each dropdown to disable it. Mouse shortcuts should already be disabled by default.)

#### "Hot Corners..." button at the bottom

This displays another modal.

Select "-" in each drop-down to disable that corner. (By default only one will be set.)

### "Keyboard" Preference Pane

* Key Repeat rate: Set it all the way to "fast".
* Delay Until Repeat: Set it all the way to "short".
* Press "fn" key to: "Do Nothing".
* "Keyboard navigation": allows you to avoid using the mouse to clear pop-ups. Enable it.

#### "Keyboard Shortcuts..." window

Click the "Keyboard Shortcuts..." button to open this.

* "Launchpad & Dock": Disable all this proprietary crap.
* "Display": Do what you want.
* "Mission Control": Disable all this proprietary crap.
* "Keyboard": Do what you want. Except for "Move focus to the next window" (Cmd-tilde), which changes windows within an app. This is absolutely essential and should be enabled. "Show contextual menu" (Ctrl-Return), which shows the right-click menu, seems useful as well.
* "Input Sources": Unless you need to type in multiple languages, disable everything here. This will free up the highly-valuable Ctrl-Space keyboard shortcut to use with your window manager.
* "Screenshots": These are too useful to change. Keep them and leave them at the defaults if you can; your programming pairs are going to expect them to work normally.
* "Presenter Overlay": I neither know nor care what this does. Disable it all.
* "Services": You need to learn other, less-proprietary ways to do everything in this menu. Disable it all.
* "Spotlight": I strongly recommend replacing Spotlight with another, more versatile, command palette program. I used to recommend Alfred, but that has been superseded by [Raycast](https://www.raycast.com/) as far as I'm concerned. If you're going to use another program, disable the Cmd-Space shortcut here so you can use it with your other program.
* "Accessibility": You know what you need in here and what you don't. You might consider enabling "Invert colors"; I find that useful on rare occasion.
* "App Shortcuts": This is so important that it gets its own subsection below.
* "Function Keys": Enable the "Use F1, F2, etc. keys as standard function keys" option. This will restore easy access to these highly useful keys. (Which some programs use by default, and can be set to useful shortcuts for other programs.) Don't worry, you can still use the keys to control volume, brightness, etc. by holding the Fn key.
* "Modifier Keys": Unless you enjoy SHOUTING when typing often, the Caps Lock key is worse than useless - it's a booby trap sitting in the middle of your keyboard. Click "Select keyboard", go through each keyboard attached to your system (internal keyboard and any USB keyboards), and remap Caps Lock to Control.

##### "App Shortcuts" section

This section of the Keyboard preference pane is important enough to get its own heading.

Click the `+` button to add or change keyboard shortcuts for menu items in various apps. You choose the application you want to modify, type the _exact_ name of the menu item you want to invoke, and press the key combination that should invoke it.

Some suggestions for things to add are below.

* All Applications:
    * "Show Help menu": Leave it activated and at its default of `Cmd-Shift-/` (a.k.a. `Cmd-?`). Incredibly powerful, because the menu opens with the "Search" box focused. This gives you a Spotlight-like search of the menus in every application, and lets you activate even menu items that have no keyboard shortcut without using the mouse. (Give it a try; I promise you'll be hooked!)
    * "Minimize": (almost?) all apps have this menu item, and it's bound to `Cmd-m` by default. It's worse than useless because it forces you to use the mouse to retrieve the window from the Dock, and `Cmd-m` is way too easy to hit accidentally. Add "Minimize" (it's not here by default) and remap it to something out-of-the-way like `Ctrl-Opt-Shift-Cmd-m`, because that's the closest you can get to disabling it altogether.
* Google Chrome:
    * "Select Next Tab": `Cmd-2` (This will override the shortcut to select the second open tab.)
    * "Select Previous Tab": `Cmd-1` (This will override the shortcut to select the first open tab.)
    * "New Window": It's `Cmd-n` by default but remap it to something out-of-the-way like `Ctrl-Opt-Shift-Cmd-N`. Why? Because you want the `Cmd-n` binding for something more powerful...
    * "Move Tab to New Window": map this to the newly-available `Cmd-n`. This will take whatever the current tab is and, well, move it to a new window. Type `Cmd-t`, `Cmd-n` and you have the same functionality as the old `Cmd-n`. It takes a little getting used to, but I find this setup far more versatile.
    * "Bookmark This Tab...": It's `Cmd-d` by default but remap it to something out-of-the-way like `Ctrl-Opt-Shift-Cmd-F6`. Why? Because you want the `Cmd-d` binding for something more powerful...
    * "Duplicate Tab": map this to the newly-available `Cmd-d`. Why? Because duplicating the current tab lets you be at two places at once within a long page. Filling out a form but need to look at something else on the page? Just duplicate the tab, find what you need, and close the duplicate. You'll be back at the form you were filling out without losing your place!
* iTerm:
    * "Reset": Destructive and too easy to hit the default binding accidentally. Remap it to something out of the way, like "Ctrl-Opt-Cmd-F6".
    * "Split Horizontally with Current Profile": You should be using a cross-platform solution like Tmux for functionality like this, and anyway it's too easy to hit the default binding accidentally. Remap it to something out of the way.
    * "Split Vertically with Current Profile": Remap it to something out of the way.
* Keynote:
    * "Previous Slide": `Cmd-Shift-[`
    * "Next Slide": `Cmd-Shift-]`

#### "Text Input" section

* "Input Sources": Click the "Edit..." button, select "All input sources", and then disable _all_ of this crap! Why on earth do they have it messing with your text as you type by default?!
* "Text Replacements...": Delete every entry in this window too! (There's only one sample by default.)

#### "Dictation" section

Unless you need dictation, turn this off with the toggle at the top. Additionally, disable the keyboard shortcut (double-press Ctrl) to avoid a popup when you press it accidentally.

### "Notifications" Preference Pane

You may want to switch certain app alert styles from "Banners" (which could go away unnoticed if you step away from your computer for a moment) to "Alerts" (which stay until you clear them). Note that an app probably won't appear in the app list here until you've launched it for the first time. (And maybe not until after the app shows you its first notification.)

Examples of apps to consider switching to "Alerts" include:

* Messages
* Slack

### "General" Preference Pane

This preference pane is rapidly becoming a junk drawer as it absorbs other preference panes. It's just a large list of sections, a few of which you'll want to visit:

#### "Sharing" section

Most of the toggles are off by default and you should probably leave them that way, with a couple exceptions:

* "Screen Sharing": This turns on VNC.
* "Remote Login": This turns on the SSH daemon and SFTP.

Also edit the "Local hostname". This includes your user name by default, which is info I'd rather not leak to the network. Rename it to [something cool](https://en.wikipedia.org/wiki/Lists_of_deities)!

#### "Login Items & Extensions" section

Some apps will set themselves up in the "Open at Login" list. For some this is great, for others it's annoying or even peformance degrading.

Consider *removing*:

* Steam

Consider adding:

* Slate or other window manager


## Set Up Apps

Hopefully your bootstrap script installed all the apps you need. If not, install them now.

### Log In to Services

Here are a few apps you're going to want to open and log into, if you have/use them.

``` text
cd /Applications
# Some other apps depend on Google Drive, so do this first!
open 'Google Drive.app'
open '1Password.app'
open 'Google Chrome.app'
open Slack.app
```

### Settings

Here are some other apps you're going to want to change specific settings in:

#### iTerm

`open /Applications/iTerm.app` and open preferences.

* "General" page
    * "Applications in terminal may access clipboard": enable
    * "Load preferences from a custom folder or URL": enable
        * Click "Browse"
        * Navigate to the folder in your dotfiles repo where you've saved your previous iTerm settings. No need to select the file itself, just the folder.
        * What?! You didn't export your previous iTerm settings?! Then you are unfortunately going to have to configure iTerm manually. Suggested settings are below. When you're done, click the "Save Current Settings to Folder" button that you see here. I recommend committing the exported settings file to your dotfiles repo. (You _do_ have [one of those](https://github.com/jaymcgavren/dotfiles), right?)
* _Note: if you loaded a previous settings file successfully, then presumably the below settings are already the way you want them. You may not need to change anything further._
* "Profiles" page
    * Select the profile you want to update, and change the settings below. Unfortunately you will have to repeat this for each profile you want to change.
    * "Keys" subpage
        * Left [option] Key: "Esc+"
        * Right [option] Key: "Esc+"

#### Google Chrome

`open '/Applications/Google Chrome.app'`.

* [Reposition Chrome Developer Tools](https://stackoverflow.com/questions/10023640/how-to-reposition-chrome-developer-tools)
* Window -> Extensions
    * Find the extensions you want available in Incognito Mode and enable them. (Not that there will be many of them; I only enabled my password manager extension.)

#### Finder

Open a Finder window.

Choose "Settings..." from the menu.

* "General" page
    * New Finder windows show: If you don't like the default Recents search, set this to a directory of your choosing.
    * Open folders in tabs instead of new windows: I hate tabs, I disabled this.
* "Sidebar" page
    * Add entries you want, like your home directory.
    * Remove entries you don't want, like tags or "iCloud Drive".
* "Advanced" page
    * Show all filename extensions: enable
    * Remove items from the Trash after 30 days: I used to do this manually and it didn't get done. Recommend enabling.
    * When performing a search: Recommend "Search the Current Folder" over the default "Search This Mac".

Now choose "File" menu, "New Finder Window". We need a window open to change the settings that follow.

* Navigate to your user's home directory. There's a special option that's only visible in that directory that we're going to want to set.
* "View" menu, "As list": enable
* "View" menu, "Show View Options"
    * We're going to set options for the currently open view, but then we'll apply them globally to all windows.
    * Always open in [selected view type] view: Ensure your preferred view type is active, then enable this.
    * Browse in [selected view type] view: Enable.
    * Group by: None
    * Sort by: Name
    * Show Columns: Recommend enabling these attributes and disabling all others:
        * Date Modified
        * Date Created
        * Size
        * Kind
    * Use relative dates: Disable.
    * Show Library Folder: This is only visible in the view options for your home directory. Enable it.
    * Use as Defaults: Click this once all options are set up the way you want, so they'll apply to other directories.

#### Screenshots

Screenshots are saved to `~/Desktop` by default. You may want to [fix that](https://www.macworld.co.uk/how-to/mac-software/change-where-mac-screenshots-saved-3682381/).

## Final thoughts

Hope you found this post helpful (and not _too_ surly)! I'm open to healthy debate about the merits of these settings. Who knows, you _might_ even change my mind about something. Leave a comment below!

<!-- ## Other -->

<!-- TODO give google chrome permission to access camera. -->
<!-- TODO give google chrome permission to access microphone. -->
