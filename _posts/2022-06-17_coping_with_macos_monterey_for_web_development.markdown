---
layout: post
title: 'Coping with MacOS Monterrey for Web Development'
tags: []
type: post
published: false
---

<!-- TODO fix line gap between nested bulleted lists -->

This is a fork of an older post I originally created for MacOS Mojave.

For pretty much every Mac I've ever owned, I've copied my configuration from machine to machine. But when one does so, a lot of unused cruft builds up over the years. So I've decided to wipe everything and start totally (well, okay, mostly) from scratch. This is a rare learning opportunity and so I'm documenting my setup here, for my reference and for yours.

This post is intended to be a living document. I'll be updating it as I discover improved settings. Comments and suggestions are welcome!

Be warned: I am an Apple skeptic. I don't like the direction recent MacOS versions have gone, and many of my settings represent an attempt to get back to "the good old days". If you're one of those fans who think Apple can do no wrong, and you want to make use of all the latest MacOS features, you may want to find another configuration guide. Now get off my lawn!

<!--more-->

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

* [Slate](https://github.com/jigish/slate): This is what I use. Open-source, configured via [text file](https://github.com/jaymcgavren/dotfiles/blob/master/slate). Not actively maintained, but it doesn't need to be; it's been in a "just works" state for years.
* [Moom](https://manytricks.com/moom/): Closed-source, $10 USD. Looks fancy, seems popular, haven't used it.
* [SizeUp](http://www.irradiatedsoftware.com/sizeup/): Closed-source, $13 USD. Seems adequate.
* [Spectacle](https://www.spectacleapp.com): Open-source. Seems adequate.


## Fix System Settings

Next, let's visit "System Preferences" to fix some terrible defaults.

### "General" Preference Pane

* Appearance: "Dark". Might help you fall asleep after a late night hacking session.

### "Security & Privacy" Preference Pane

On the "General" page: Require password after sleep or screen saver begins: 5 seconds

### "Trackpad" Preference Pane

#### "Point & Click" page

* Look up & data detectors: Disable. I don't want my trackpad doing random useless stuff because I clicked "too hard".
* Secondary click: Disable. I don't want my trackpad doing random stuff because I didn't lift a finger.
* Tap to click: Disabled by default and needs to stay that way. Why is this crap even a setting?!
* Force Click and haptic feedback: Disable.

#### "Scroll & Zoom" page

* Scroll direction: Natural: Disable. Enabling it seems fine on a trackpad but in my experience it reverses a mouse scroll wheel too, which is not fine.
* Other settings: I'm leaving these at the default (enabled), until such time as they piss me off.

#### "More Gestures" page

Disable all this crap! Mission Control, Exposé, Launchpad, all of it. Here's why:

* These features only exist on MacOS (at least in this exact form). Get too used to them and you won't be willing/able to switch to another OS when the time comes.
* These gestures can be invoked accidentally.
* They're only there for damn dirty mouse/trackpad users. _You_ don't have time for that; you use your keyboard and a window manager.

### "Dock & Menu Bar" Preference Pane

* The dock is for damn dirty mouse/trackpad users, not for you. I don't think it can be disabled entirely with stock software (please let me know if I'm wrong) but you can minimize how much it gets in the way.
* Size: minimum
* Magnification: disable
* Position on screen: Leave at default of "Bottom".
* Double click a window's title bar to: Disable this. You should be using a window management program to minimize/maximize windows.
* Automatically hide and show the Dock: Enable so that at least it's hidden most of the time.

### "Mission Control" Preference Pane

Don't use Mission Control. Habituation to it promotes vendor lock-in with Apple. It's for damn dirty mouse/trackpad users anyway. You're going to use a window manager that lets you keep your hands on the keyboard.

The directions [here](https://web.archive.org/save/https://www.amsys.co.uk/how-to-disable-mission-control-and-spaces-in-os-x/) for disabling Mission Control entirely _used_ to work (as of MacOS 10.14.6). Now they don't. The best you can do is disable everything in this preference pane:

* Disable all the check boxes.
* Under "Keyboard and Mouse Shortcuts", disable all shortcuts:
    * Mission Control: select `-` from the dropdown.
    * Application windows: select `-` from the dropdown.
    * Show Desktop: leave at the default, blank. Or if that doesn't work, select `-`.

### "Keyboard" Preference Pane

#### "Keyboard" page

* Key Repeat rate: Max it out.
* Delay Until Repeat: Minimize it.
* Touch Bar shows: I've never used the Touch Bar and I refuse to start. Change it to show "F1, F2, etc." This also gets your Esc "key" back. The whole setup still sucks because there's no tactile key press, but at least now it won't randomly change functions on you.
* If you're lucky enough to have a newer machine that got rid of the stupid Touch Bar and has function keys back again, you should see a "Use F1, F2, etc. keys as standard function keys" option. You want it enabled (which it should be by default).
* Unless you enjoy SHOUTING when typing often, the Caps Lock key is worse than useless - it's a booby trap sitting in the middle of your keyboard. Click the "Modifier Keys..." button, and remap Caps Lock to Control.

#### "Text" page

* Uncheck everything here! Why on earth do they have it messing with your text as you type by default?!
* Be sure to click the "-" button to remove any "Replace/With" text expansions, too.

#### "Shortcuts" page

* "Use keyboard navigation to move focus between controls": allows you to avoid using the mouse to clear pop-ups. Enable it.
* "Launchpad & Dock" section:
    * Turn Dock Hiding On/Off: disable
* "Mission Control" section:
    * Move left/right a space: disable these
* "Keyboard" section:
    * Change the way Tab moves focus: disable
    * Move focus to the Dock: disable
* "Accessibility" section:
    * Invert colors: enable

##### "App Shortcuts" section

This section of the Keyboard preference pane is important enough to get its own heading.

Click the `+` button to add or change keyboard shortcuts for menu items in various apps. You choose the application you want to modify, type the _exact_ name of the menu item you want to invoke, and press the key combination that should invoke it.

Some suggestions for things to add are below.

* All Applications: [Re-map the Minimize command to something you won't press accidentally.](https://apple.stackexchange.com/questions/115562/how-do-i-disable-the-minimize-command-m-shortcut-in-mavericks)
* Google Chrome:
    * "Select Next Tab": `Cmd-2` (This will override the shortcut to select the second open tab.)
    * "Select Previous Tab": `Cmd-1` (This will override the shortcut to select the first open tab.)
* Keynote:
    * "Previous Slide": `Cmd-Shift-[`
    * "Next Slide": `Cmd-Shift-]`

### "Notifications" Preference Pane

You may want to switch certain app alert styles from "Banners" (which could go away unnoticed if you step away from your computer for a moment) to "Alerts" (which stay until you clear them). Examples include:

* Messages
* Slack

### "Sharing" Preference Pane

* Computer Name: This includes your user name by default, which is info I'd rather not leak to the network. Rename it to [something cool](https://en.wikipedia.org/wiki/Lists_of_deities)!

### "Users & Groups" Preference Pane

#### "Login Items" page

* Some apps will set themselves up to open on login. For some this is great, for others it's annoying or even peformance degrading.
* Consider removing:
    * Amazon Music
    * Steam
* Consider adding:
    * Slate or other window manager


## Set Up Apps

Hopefully your boostrap script installed all the apps you need. If not, install them now.

Here are a few apps you're going to want to open and log into, if you have/use them.

``` text
cd /Applications
open 'Dropbox.app' # Some other apps depend on DropBox, so do this first!
open '1Password 6.app' # Why the hell do they put the version in the .app name?!
open 'Google Chrome.app'
open Slack.app
```

Here are some other apps you're going to want to change specific settings in:

* `open /Applications/iTerm.app`
    * Preferences
        * "General" page
            * "Applications in terminal may access clipboard": enable
            * "Load preferences from a custom folder or URL": enable
                * Click "Browse"
                * Navigate to the folder in your dotfiles repo where you've saved your previous iTerm settings. No need to select the file itself, just the folder.
                * What?! You didn't export your previous iTerm settings?! Then you are unfortunately going to have to configure iTerm manually. Suggested settings are below. When you're done, click the "Save Current Settings to Folder" button that you see here. I recommend committing the exported settings file to your dotfiles repo. (You _do_ have [one of those](https://github.com/jaymcgavren/dotfiles), rinnght?)
        * _Note: if you loaded a previous settings file successfully, then presumably the below settings are already the way you want them. You may not need to change anything further._
        * "Profiles" page
            * Select the profile you want to update, and change the settings below. Unfortunately you will have to repeat this for each profile you want to change.
            * "Keys" subpage
                * Left [option] Key: "Esc+"
                * Right [option] Key: "Esc+"
* `open '/Applications/Google Chrome.app'`
    * [Reposition Chrome Developer Tools](https://stackoverflow.com/questions/10023640/how-to-reposition-chrome-developer-tools)
    * Window -> Extensions
        * Find the extensions you want available in Incognito Mode and enable them. (Not that there will be many of them; I only enabled 1Password.)
* Finder
    * Preferences
        * "General" page
            * New Finder windows show: If you don't like the default Recents search, set this to a directory of your choosing.
            * Open folders in tabs instead of new windows: I hate tabs, I disabled this.
        * "Sidebar" page
            * Add entries you want, like your home directory.
            * Remove entries you don't want, like tags or "iCloud Drive".
        * "Advanced" page
            * Show all filename extensions: enable
            * Remove items from the Trash after 30 days: I used to do this manually and it didn't get done. Recommend enabling.
    * "File" menu, "New Finder Window". We need a window open to change the settings that follow.
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
        * Show Library Folder: This is only visible in the view options for your home directory. Enable it.
        * Use as Defaults: Click this once all options are set up the way you want, so they'll apply to other directories.
* Screenshots are saved to `~/Desktop` by default. You may want to [fix that](https://www.macworld.co.uk/how-to/mac-software/change-where-mac-screenshots-saved-3682381/).

Hope you found this post helpful (and not _too_ surly)! I'm open to healthy debate about the merits of these settings. Who knows, you _might_ even change my mind about something. Leave a comment below!

<!-- ## Other -->

<!-- TODO give google chrome permssion to access camera. -->
<!-- TODO give google chrome permssion to access microphone. -->
