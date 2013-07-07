---
layout: post
title: Those still using DRb...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '646'
  original_post_id: '673'
  _wp_old_slug: '673'
---
Make sure the libraries your client will be using are loaded on the server side as well.  You'll save yourself an evening of hair-tearing debugging.

zyps_server is back, and a full-fledged executable now.  Running your own classes is horribly broken (you have to use what's loaded on the server), but if you're not using DRbUndumped your creatures will operate <em>very</em> fast on the host (because copies are created on the server side).  No need to keep your client running, either - just add the objects to the remote environment and terminate, and they'll live on in the server.

I'll be showing this off at the next Ruby Users Group, and I'll encourage everyone to connect and play around.  It'll be interesting to see what people come up with.
