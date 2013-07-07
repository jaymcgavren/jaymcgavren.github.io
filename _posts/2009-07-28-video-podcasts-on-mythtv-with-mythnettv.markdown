---
layout: post
title: Video podcasts on MythTV with MythNetTV
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1034'
  original_post_id: '1242'
  _wp_old_slug: '1242'
---
<a href="http://www.stillhq.com/mythtv/mythnettv/">MythNetTV</a> is an early but effective MythTV extension that downloads podcasts and adds them to your recordings list, just like the free downloads feature on TiVo (except you can subscribe to anything you want, provided the format's supported).

These commands will install and configure the app (be sure to substitute the path you want videos saved to):

<pre>
sudo apt-get install mythnettv
mkdir /your/dir/here
mythnettv --datadir=/your/dir/here
</pre>

Subscribe to some geeky shows:

<pre>
mythnettv subscribe "http://revision3.com/pixelperfect/feed/Xvid-Small" "PixelPerfect"
mythnettv subscribe "http://www3.youtube.com/rss/global/top_rated.rss" "YouTubeTopRated"
mythnettv subscribe "http://revision3.com/trs/feed/Xvid-Small" "TotallyRadShow"
mythnettv subscribe "http://applebytepodcast.cnettv.com/" "CnetAppleByte"
mythnettv subscribe "http://buzzreportpodcast.cnettv.com/" "CnetBuzzReport"
mythnettv subscribe "http://cnetnewspodcast.cnettv.com/" "CnetNewsDaily"
mythnettv subscribe "http://firstlookpodcast.cnettv.com/" "CnetFirstLook"
mythnettv subscribe "http://hackspodcast.cnettv.com/" "CnetHacks"
mythnettv subscribe "http://howtopodcast.cnettv.com/" "CnetHowTo"
mythnettv subscribe "http://realdealvideopodcast.cnettv.com/" "CnetRealDeal"
mythnettv subscribe "http://revision3.com/coop/feed/Xvid-Small" "Co-Op"
mythnettv subscribe "http://www.onnetworks.com/feeds/1460/video/rss.xml?target=site" "PlayValue"
</pre>

Get show lists for all subscriptions, then download 10 shows:

<pre>
mythnettv update
mythnettv download 10
</pre>

List the next 10 shows that will be downloaded:

<pre>
mythnettv nextdownload 10
</pre>

Download 1 show from the given subscription:

<pre>
mythnettv download 1 CnetNewsDaily
</pre>

List subscriptions:

<pre>
mythnettv list
</pre>

More info on these commands and others:

<pre>
man mythnettv
</pre>
