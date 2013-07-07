---
layout: post
title: Slap to forehead...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  original_post_id: '344'
  _wp_old_slug: '344'
---
I've been trying to figure out why the new features in yesterday's software release wasn't working - at all.

-I checked the release checksums (which tell you that the files installed are the versions you think they are).  They matched.
-I re-ran my unit tests to see if the new features worked in development.  They did.
-I pored over the source code to see what could have caused it to fail in production.  I didn't find anything.
-Eventually, I was trying pretty much random stuff - I went to the production server and looked at the date on the executable file.  ...April 3rd?!

Finally, after more searching, I figured it out - Operations had installed the new version correctly... on the wrong server.  Per my instructions.

My release scripts auto-generate deployment instructions (because you can only type the damn thing so many times before you want to kick in your monitor).  I had copied the config from a different project, without changing the server name.

Tiny mistake, made to look very big by our tedious release process.  When do I get to just sit down and write code again?
