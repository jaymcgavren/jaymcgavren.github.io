---
layout: post
title: MP3 conversions of Ruby conference videos...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1098'
  original_post_id: '1421'
  _wp_old_slug: '1421'
---
I've got a sizable commute, so I've taken to downloading conference videos and converting to MP3 to play in the car.  Most work reasonably well as speech-only, I'm finding.  In hopes of helping others, I'm posting them here.

Many thanks to Confreaks, the conference organizers, and to the generous speakers, who released their speeches under a Creative Commons license.  In accordance with the license of the original videos, these MP3s are also released under a <a href="http://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-ShareAlike license</a>.

<a href="http://jay.mcgavren.com/files/conference_mp3s/">Download MP3 conversions of Confreaks conference videos here.</a>

You can automatically download the lot with wget if you have it installed:

<pre>
wget --recursive --no-parent --accept mp3,ogg,MP3,OGG http://jay.mcgavren.com/files/conference_mp3s
</pre>

Conversions were done with ffmpeg.  Here's the script I used:

<pre>
#!/bin/sh
for filename; do
    ffmpeg -i "${filename}" -acodec libmp3lame -ab 96k -ac 2 -ar 44100 "${filename}.mp3"
done
</pre>

My chief complaint was wild variation in volume levels; I haven't blown a speaker yet but loud noises have made me jump sometimes.  I've processed all these with "mp3gain" (which I thought was only available as a Windows GUI app but have since learned has a Linux command-line version) in an effort to correct this, but I make no guarantees there won't be sudden jumps or drops in volume.

Many tweaks are still possible, and I will look into them if there's demand:

<ul>
<li>Remove the periods of silence on each track (where Confreaks originally showed sponsor logos).</li>
<li>Convert remaining videos (these were hand-picked).</li>
<li>Lower-bitrate versions for the space-conscious.</li>
<li>See if The Levelator produces better results than mp3gain.</li>
<li>ID3 tags with speakers, titles, and other metadata.</li>
<li>An actual podcast feed.</li>
</ul>

Enjoy, and leave a comment with the improvements you'd like to see!
