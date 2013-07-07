---
layout: post
title: Quick setup for Linux games under MythTV/MythGame...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1030'
  original_post_id: '1236'
  _wp_old_slug: '1236'
---
These commands will install some quality games that can be played full-screen:

<pre>
sudo apt-get install a7xpg
sudo apt-get install gunroar
sudo apt-get install kobodeluxe
sudo apt-get install parsec47
sudo apt-get install rrootage
sudo apt-get install sdl-ball
sudo apt-get install titanion
sudo apt-get install torus-trooper
sudo apt-get install tumiki-fighters
</pre>

This command will add a "Native" games entry under the Games menu.  You'll be prompted for your MythTV DB password, which is likely stored in "/etc/mythtv/mysql.txt".

<pre>mysql --database=mythconverg -u mythtv -p -e "INSERT INTO gameplayers (playername, gametype, commandline, rompath, extensions) VALUES ('Native', 'Other', '', '$HOME/bin/games', '');"</pre>

Then fill $HOME/bin/games "ROM directory" with scripts that launch each respective game.  (These are set up for a control pad and 1024x768 resolution, so they may need tweaking.)

<pre>
~/bin/games/titanion
#!/bin/sh
titanion -fullscreen -res 1024 768

~/bin/games/gunroar
#!/bin/sh
gunroar -fullscreen -res 1024 768 -enableaxis5

~/bin/games/rrootage
#!/bin/sh
rrootage -fullscreen -lowres

~/bin/games/parsec47
#!/bin/sh
parsec47 -fullscreen -lowres

~/bin/games/torus-trooper
#!/bin/sh
torus-trooper -fullscreen -res 1024 768

~/bin/games/a7xpg
#!/bin/sh
a7xpg -fullscreen -lowres

~/bin/games/sdl-ball
#!/bin/sh
sdl-ball

~/bin/games/kobo-deluxe
#!/bin/sh
kobodl -fullscreen -width 1024 -height 768 -joystick -nomusic

~/bin/games/tumiki-fighters
#!/bin/sh
tumiki-fighters -fullscreen -res 1024 768
</pre>

Be sure to make the scripts executable, or they won't launch:

<pre>chmod ugo+x ~/bin/games/*</pre>

In mythfrontend, go into game setup and scan for new games.  Each script you set up should then appear under the "Native" entry in the games menu - just pick one and fire away.

Questions/suggestions?  Post 'em in the comments!
