---
layout: post
title: Oh, for Pete's sake...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1056'
  original_post_id: '1301'
  _wp_old_slug: '1301'
---
This is what my evening has been like...

<pre>
Spec::Mocks::MockExpectationError in 'ResourceManager#load_resources with global assets loads gif files'
# expected :cache_image with (:test, "test/data/loads_png/test.png")
but received it with (:gif, "test/daUnknown type of file: test/data/state_specific/.DS_Store
Unknown type of file: test/data/state_and_global/.DS_Store
ta/loads_gif/gif.gif")
./src/managers/resource_manager.rb:19:in `load_resources'
./src/managers/resource_manager.rb:11:in `each'
./src/managers/resource_manager.rb:11:in `load_resources'
test/unit/managers/resource_manager_spec.rb:38:
</pre>

Grumble, grumble...  <em>fix</em>

<pre>
Spec::Mocks::MockExpectationError in 'ResourceManager#load_resources with global assets loads gif files'
# expected :cache_image with (:test, "test/data/loads_gif/test.gif")
but received it with (:gif, "test/data/loads_gif/gif.gif")
</pre>

GRUMBLE grumble grumble...  <em>fix</em>

<pre>
Spec::Mocks::MockExpectationError in 'ResourceManager#load_resources with global assets loads gif files'
# expected :cache_image with (:test, "test/data/loads_gif/gif.gif")
but received it with (:gif, "test/data/loads_gif/gif.gif")
</pre>

#$#@$#@#$#$@$#@$@#!!!!
