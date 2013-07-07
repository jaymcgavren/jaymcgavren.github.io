---
layout: post
title: QuickSilver Google search with 100 results per page...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1005'
  original_post_id: '1192'
  _wp_old_slug: '1192'
---
Man, was this a pain to find.  I'm assuming some proficiency with XML and Quicksilver here; leave a comment if you need more specific directions.

Install the Web Search module from the Quicksilver plugins pane if you haven't already.  Quit Quicksilver.  Then edit this file:

<pre>
~/Library/Caches/Quicksilver/Indexes/QSPresetDocWebSearches.qsindex
</pre>

Search for:
<pre>
&lt;string&gt;qss-http://www.google.com/search?hl=en&amp;q=***&lt;/string&gt;
</pre>

And change it to:
<pre>
&lt;string&gt;qss-http://www.google.com/search?hl=en&amp;q=***&amp;num=100&lt;/string&gt;
</pre>

Be sure you've got the "Google Search" entry; there are many similar ones.  I originally edited the file while Quicksilver was running and had to quit and reload the catalog several times before I got it to stick.  Your mileage may vary.

To test, bring up QS, type "Google Search", tab twice, type your query, and press Return.  Your default browser should load a Google Search with 100 results per page.  You can of course make any other tweaks to this or any other search URL that your heart desires.
