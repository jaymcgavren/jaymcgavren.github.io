---
layout: post
title: RailsConf notes - Kevin Barnes - In Praise of Non-Fixtured data
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1009'
  _oembed_66565bf1d4e41051cbdfcdee3b97ab22: '{{unknown}}'
  _oembed_d01b8f6ccb45b32f0208ba84103be6a7: '{{unknown}}'
  original_post_id: '1198'
  _wp_old_slug: '1198'
---
<pre>
Fixtures bad:
	Get highly unmanageable, especially when someone decides to import real data (:user_275, :user_276...)
	Live outside test.
	Can't change loaded values easily.
Factories good:
	Let you use sensible labels and tweak the created data.
	They reduce dependence on external data (manipulate values right in the test).
FactoryGirl:
	http://github.com/thoughtbot/factory_girl/tree/master
	spec/factories/first_model.rb second_model.rb...
	Code:
		Factory.define :user {|f| f.name 'Joe'; f.zip '34279'; f.association :employer}
		Factory(:user).should be_valid
		Factory(:user, :name =&gt; nil).should_not be_valid
	.association calls another factory (that you define) to generate associated model object.
Object Daddy:
	http://github.com/flogic/object_daddy/tree/master
	spec/exemplars/*_exemplar.rb
	Code:
		class User
			generator_for :name =&gt; 'Test User'
			generator_for :ssn, :start =&gt; '12343214' do {|prev| prev.succ}
		end
		@user = User.generate!
		@user.should be_valid
	[Barnes likes ObjectDaddy.  I don't 'cause of modificat
Others:
	machinist
	foundry
	fixjour
</pre>
