---
layout: post
title: Notes from RailsConf - ActiveScaffold BoF session...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1010'
  original_post_id: '1199'
  _wp_old_slug: '1199'
---
Thanks to Mike Gaffney and Kenney Ortmann for hosting this session, and for writing a cool framework!

<a href="http://activescaffold.com/">http://activescaffold.com/</a>

<pre>
Install:
        script/plugin install
        git://github.com/activescaffold/active_scaffold.git
        Site says to pass -r rails-2.2 option; HEAD works fine for Rails 2.3.

Setting up a quick test app in Rails 2.3:
        Create app/views/layouts/application.html.erb:
                Ensure it contains a default HTML document.
                Ensure it has  in the body.
        Add these lines to the HEAD tag:
                
                
        Create a model with a few fields and a controller.
        On your controller, add:
                active_scaffold :model_name
        Go view the index for the model (no need to create index.html.erb, def
        index, etc.):
                You should have full CRUD, sorting by column, etc.

Customizing:
        ActiveScaffold.set_defaults {|config| ...} in your application
        controller.
        Model-specific settings in individual controllers.
        Override ActiveScaffold's default views by creating a special folder in
        your views directory.

Additional notes:
        Home page doesn't get updated as often as it should, but project is
        being actively maintained and used, and will support Rails 3.0 shortly
        after its release.
        For many-to-many relationships, you may need to have the view reference
        the join model.  See the mailing list.
</pre>

Had this up and running in 10 minutes:

<a href='http://jay.mcgavren.com/blog/wp-content/uploads/2009/05/picture-23.png' title='ActiveScaffold'><img src='http://jay.mcgavren.com/blog/wp-content/uploads/2009/05/picture-23.thumbnail.png' alt='ActiveScaffold' /></a>
