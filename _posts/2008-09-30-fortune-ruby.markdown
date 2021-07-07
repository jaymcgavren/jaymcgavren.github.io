---
layout: post
title: $ fortune ruby
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '934'
  original_post_id: '1061'
  _wp_old_slug: '1061'
---
More often than I'd like, I have to open the Pickaxe to look up a core class or module that I can't quite remember the methods on.  I wanted to put some reminders in a place I could review them daily, yet was unobtrusive.

Enter the Phosphor screensaver for X-Windows; it scrolls text from a file or command by the screen.  I pulled the classes and modules I wanted from the "ri" utility, made them into a "fortune cookie file" (run "man fortune" for details on fortune), and then piped fortune's output through the screensaver.

I've attached the files I made.  Unzip and drop them in /usr/share/games/fortune (or wherever fortune cookie files go on your system) and you'll be able to type "fortune ruby" at a command prompt.  Only core classes are included, but I'll make a separate one for Rails on request.  You can set up Phosphor (or other text-display screensavers like StarWars) from the xscreensaver control panel.

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2008/09/ruby.zip' title='RubyFortuneCookies'>RubyFortuneCookies</a>

<em>Edit:</em> On systems using gnome-screensaver, save this in your screensaver config folder, probably as /usr/share/applications/screensavers/xscreensaver-phosphor-ruby.desktop:

``` text
[Desktop Entry]
Encoding=UTF-8
Name=Phosphor - Ruby ri
Comment=Draws a simulation of an old terminal, with large pixels and long-sustain phosphor. On X11 systems, This program is also a fully-functional VT100 emulator! Written by Jamie Zawinski; 1999.
TryExec=phosphor
Exec=phosphor -root -scale 2 -ticks 5 -program 'fortune ruby'
StartupNotify=false
Type=Application
Categories=GNOME;Screensaver;
```

...then select "Phosphor - Ruby ri" in your Screensaver Preferences.  This should also scale back the text so you can see the whole ri screen.
