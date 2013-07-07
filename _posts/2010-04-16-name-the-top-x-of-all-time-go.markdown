---
layout: post
title: Name the Top X of All Time - go!
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1089'
  original_post_id: '1407'
  _wp_old_slug: '1407'
---
A friend asked for a quick script to help him sort a top-50 list of games.  Here's what I threw together:

{% highlight ruby %}
#!/usr/bin/env ruby

# rank.rb - Rank a list of items, two at a time.

# Copyright (c) 2010 Jay McGavren
#
# Permission is hereby granted, free of charge, to any person obtaining
# a copy of this software and associated documentation files (the
# "Software"), to deal in the Software without restriction, including
# without limitation the rights to use, copy, modify, merge, publish,
# distribute, sublicense, and/or sell copies of the Software, and to
# permit persons to whom the Software is furnished to do so, subject to
# the following conditions:
#
# The above copyright notice and this permission notice shall be
# included in all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
# LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
# OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
# WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


require 'fileutils'
require 'curses'

file_name = ARGV[0] or fail "Usage: #{__FILE__} filename.txt"

def random_index(list)
  rand(list.length)
end

def write_store(name, entries)
  File.open(name, 'w+') do |file|
    file.puts(entries)
  end
end

def read_store(name)
  entries = []
  File.open(name) do |file|
    entries = file.readlines
  end
  entries
end

entries = read_store(file_name)

Curses.noecho
Curses.init_screen
Curses.stdscr.keypad(true)

loop do
  # Pick 2 random items.
  indices = [0, 0]
  while (indices[0] == indices[1]) do
    indices = [random_index(entries), random_index(entries)]
  end
  indices.sort!
  # Present them.
  Curses.setpos(0, 0)
  Curses.addstr(<<-EOD)
    Which is better?
    1. #{entries[indices[0]]}
    2. #{entries[indices[1]]}
    3. Exit
  EOD
  begin
    result = nil
    until ([?1, ?2, ?3].include?(result)) do
      result = Curses.getch
    end
    case result
    # Higher one chosen?
    when ?1
      # Do nothing.
    # Otherwise:
    when ?2
      # Swap them.
      entries[indices[0]], entries[indices[1]] = entries[indices[1]], entries[indices[0]]
    # Exit chosen?
    when ?3
      # Exit loop.
      break
    else
      fail "wtf?"
    end
  end
  write_store("#{file_name}.bak", entries)
end

# Save.
FileUtils.mv("#{file_name}.bak", file_name)

Curses.close_screen
{% endhighlight %}

It picks two entries at random, and swaps their positions if you choose the later one as your favorite.  Lather, rinse, repeat.  Like a bubble sort without adjacent items.

Curses?  Well, it was the quickest way to get Ruby to respond to a single keypress.  And since you're going to be making a lot of entries, I didn't want you to have to hit Enter after every one.

So here you see my list of artists with 5-star songs, originally in alphabetical order, but with my favorites starting to bubble to the top:

<!--more-->

* 10,000 Maniacs
* Enigma
* Boom Boom Satellites
* Alpha
* Amon Tobin
* Aphex Twin
* Barenaked Ladies
* Arovane
* Audioslave
* Boards of Canada
* Massive Attack
* Red Snapper
* Tipper
* Beach Flea
* Cake
* Ben Folds Five
* Counting Crows
* Propellerheads
* Billy Joel
* The Smashing Pumpkins
* Lemon Jelly
* Fatboy Slim
* Boards Of Canada
* Shpongle
* Bola
* Coldplay
* Weekend Players
* Boulderdash
* Buckethead
* Crunch
* Ulrich Schnauss
* Basement Jaxx
* µ-Ziq
* Dol-lop
* Chicane
* Depeche Mode
* Clint Mansell
* Train
* Boom Bip
* Bent
* Creed
* Beck
* Cujo
* DJ Cam
* Röyksopp
* Daft Punk
* Red Hot Chili Peppers
* Death Cab for Cutie
* Plaid
* Deftones
* Delarosa &amp; Asora
* Christian Kleine
* Caviar
* Third Eye Blind
* Duncan Sheik
* E.S. Posthumus
* Eat Static
* The Crystal Method
* 3 Doors Down
* Blind Melon
* Fluke
* Hive
* BT
* Loden
* Goldie
* Groove Armada
* Hexstatic
* R.E.M.
* Hybrid
* Bush
* Sugar Ray
* Jay McGavren
* Single Cell Orchestra
* Kenji Kawai
* LFO
* Saru
* Sarah McLachlan
* Arkarna
* Prefuse 73
* James Bong
* Lusine ICL
* Banco de Gaia
* Mighty Dub Cats
* Mike &amp; Rich
* The Cranberries
* Natalie Merchant
* Orbital
* P.M. Dawn
* Clue to Kalo
* Pearl Jam
* Photek
* Deep Forest
* Polygon Window
* Portishead
* Loess
* Prince
* Proem
* Billie Myers
* Freaky Chakra
* Dave Matthews Band
* Global Communication
* Roni Size &amp; Reprazent
* DJ Krush
* Moby
* Blessid Union of Souls
* Londonbeat
* Savath &amp; Savalas
* Seal
* The Chemical Brothers
* Shantel
* Genesis
* Jimpster
* Elton John
* The Wiseguys
* Living Colour
* Stone Temple Pilots
* Janet Jackson
* Talvin Singh
* Blackwatch &amp; Greed
* Squarepusher
* Soundgarden
* The Dust Brothers
* The Postal Service
* The Prodigy
* Seb &amp; Lo-tec
* Spring Heel Jack
* Dot Allison
* Isao Tomita
* Patchwork
* Bôa
* A Man Called Adam
* wunsch/demmin
* Chicago

Been meaning to write something like this for a while, and my friend's request was just the final nudge.  Hopefully this will help others looking for something similar.
