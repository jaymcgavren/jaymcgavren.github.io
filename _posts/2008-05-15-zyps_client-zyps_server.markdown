---
layout: post
title: zyps_client, zyps_server...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '825'
  original_post_id: '921'
  _wp_old_slug: '921'
---
OK, here we go.  The window on the left is the server, and on the right is the client.  The server has absolute authority on all object movement right now, so objects on the client will occasionally "snap" back into the places dictated by the server.  (That's the jagged part in the trails on the client; the smaller boundary on the server causes them to change direction on the server only, and fall out of sync momentarily.)  The shells in the background are both barfing debug data.

Next up is to test with multiple clients, and with joining/leaving whenever the client wants.  I also need to get back the same degree of freedom for live coding that dRuby offered (shouldn't be too difficult).

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2008/05/zyps_server_client.png' title='zyps_server_client.PNG'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2008/05/zyps_server_client.thumbnail.PNG' alt='zyps_server_client.PNG' /></a>
