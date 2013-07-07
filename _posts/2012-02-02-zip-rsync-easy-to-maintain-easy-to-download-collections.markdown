---
layout: post
title: Zip + RSync = Easy to Maintain, Easy to Download Collections
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1123'
  original_post_id: '1489'
  _wp_old_slug: '1489'
---
Most people who've used a command line know about the existence of the "zip" utility.  It's basically a scriptable version of the archive tools we all use in our file browsers.  Hopefully most people also know about <a href="http://everythinglinux.org/rsync/">RSync</a>, which brings a directory structure into sync on two machines by creating, deleting, and updating files as necessary.

What people may <em>not</em> know, however, is that RSync will transmit only the updated portions of a file if it already exists on the remote side.  That means you can easily maintain downloadable .zip archives, so your audience can retrieve whole collections of files at once.  (Say, of your <a href="/blog/archives/1488">favorite Creative Commons-licensed music</a>, which is the example we'll use here.)

We start with a command line to add MP3s to a .zip file:

<pre>
$ zip ~/Documents/media/cc_music.zip 
/Users/jay/Music/iTunes/iTunes Music/Ghost/ccMixter/Lullaby.mp3
</pre>

The long music path is for convenience - that way I can just drag-and-drop files onto a terminal.  It's a nice touch that the full folder structure is preserved (though I will likely want to strike the "Users/jay" directory at some point):

<pre>
$ unzip -l ~/Documents/media/cc_music.zip
Archive:  /Users/jay/Documents/media/cc_music.zip
 Length     Date   Time    Name
 --------    ----   ----    ----
 3664924  06-26-11 00:58   Users/jay/Music/iTunes/iTunes
Music/Ghost/ccMixter/Lullaby.mp3
...
</pre>

If we use `&&` to add on an rsync command, the .zip file will automatically be sent to the remote server if compression is successful:

<pre>
$ zip ~/Documents/media/cc_music.zip
/Users/jay/Music/iTunes/iTunes Music/Ghost/ccMixter/Lullaby.mp3 &amp;&amp; 
rsync --verbose --compress ~/Documents/media/cc_music.zip 
jay.mcgavren.com:files/cc_music.zip
</pre>

In the output, we can see the file being zipped, followed by the rsync transmission info:

<pre>
 adding: Users/jay/Music/iTunes/iTunes
Music/Ghost/ccMixter/Lullaby.mp3 (deflated 3%)
cc_music.zip

sent 3556109 bytes  received 31 bytes  78156.92 bytes/sec
total size is 3554835  speedup is 1.00
</pre>

Keeping all this as one command allows automatic updates of the remote file as new MP3s are added:

<pre>
$ zip ~/Documents/media/cc_music.zip 
/Users/jay/Music/iTunes/iTunes Music/DoKashiteru/ccMixter/Our
Slanted Voices (ft. Colin Mutchler).mp3 &amp;&amp; 
rsync --verbose --compress ~/Documents/media/cc_music.zip 
jay.mcgavren.com:files/cc_music.zip
 adding: Users/jay/Music/iTunes/iTunes Music/DoKashiteru/ccMixter/Our
Slanted Voices (ft. Colin Mutchler).mp3 (deflated 1%)
cc_music.zip

sent 5043684 bytes  received 11377 bytes  306367.33 bytes/sec
total size is 8595106  speedup is 1.70
</pre>

Those transmission sizes represent only the new MP3 that's been added, not the whole archive.  For example, if I add a small README.txt to the archive...

<pre>
$ zip ~/Documents/media/cc_music.zip README.txt &amp;&amp; 
rsync --verbose --compress ~/Documents/media/cc_music.zip 
jay.mcgavren.com:files/cc_music.zip
 adding: README.txt (deflated 36%)
cc_music.zip

sent 1288 bytes  received 20521 bytes  3965.27 bytes/sec
total size is 11636110  speedup is 533.55
</pre>

...note that only 1KB (of the now-11MB file) is actually transmitted.  Updates to files in the middle of the archive likewise cause the retransmission of only that file's zipped content.

This can of course be converted to a shell script, but personally I think doing it all at the prompt lends itself to ad-hoc, on-the-fly alterations.  (I wouldn't want a script sitting around for every collection I could think to post.)

And I can certainly think of a lot of things to share this way - Project Gutenberg books, Creative Commons wallpapers, your own photos, basically anything that you can freely redistribute.  Some care needs to be taken with variance in licenses (I had to add attribution ID3 tags to some of the MP3s, for example).  But generally, it should be possible to include the needed documentation in the archive alongside the content.  (I am not a lawyer, this is not legal advice, etc. etc.)

I view this as vastly preferable to clicking though dozens of <a href="http://archive.org">archive.org</a> pages to manually download individual files.  If you agree, I hope you'll use this technique to start sharing your own collections!
