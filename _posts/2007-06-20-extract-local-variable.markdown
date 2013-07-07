---
layout: post
title: Extract local variable...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '546'
  original_post_id: '516'
  _wp_old_slug: '516'
---
Eclipse just saved me a couple hours' work...  Thanks to a series of admittedly bad decisions, I had a unit test chock full of call chains like this:

<pre>
assertEquals("West", hc.getAreaInfo().getAttractions().getAttraction().get(3).getRefPoints().getRefPoint().get(0).getDirection());
assertEquals("Name", hc.getAreaInfo().getAttractions().getAttraction().get(3).getRefPoints().getRefPoint().get(0).getName());
assertEquals("20",   hc.getAreaInfo().getAttractions().getAttraction().get(3).getRefPoints().getRefPoint().get(0).getTransportations().getTransportation().get(0).getTransportationCode());
//...etc
</pre>

....too embarrassing to let a colleague see.  So I was resigned to spending a very boring midday importing the appropriate classes and assigning those values to local variables, when it occurred to me to check Eclipse's Refactor menu...

And there I found "Extract local variable".  What a godsend.  All I had to do was highlight the section of the call chain I wanted, and it (intelligently) chose a variable name, replaced all occurrences with the variable, and even imported the classes I needed.  In just a few minutes the above code and everything like it was changed to this:

<pre>
com.mycompany.ota.generated.AreaInfoType.Attractions.Attraction attraction = hc.getAreaInfo().getAttractions().getAttraction().get(3);
RefPoint refPoint = attraction.getRefPoints().getRefPoint().get(0);
assertEquals("West", refPoint.getDirection());
assertEquals("Name", refPoint.getName());
assertEquals("20",   refPoint.getTransportations().getTransportation().get(0).getTransportationCode());
//...etc
</pre>

Java is a very bad language, and Eclipse is what was created to cope with it.  Fortunately, its creators exhibit boundless ingenuity.
