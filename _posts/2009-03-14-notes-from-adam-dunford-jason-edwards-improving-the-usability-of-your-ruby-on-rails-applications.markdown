---
layout: post
title: 'Notes from Adam Dunford & Jason Edwards: Improving the Usability of Your Ruby
  on Rails Applications'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '998'
  original_post_id: '1182'
  _wp_old_slug: '1182'
---
<pre>
Usability: Can a user accomplish THEIR goal?
Use actual users in usability testing.
Investment in usability usually offers 10x-100x return in increased profit.
Creating structure:
	Organize
	Prioritize
		Most important stuff is most obvious
	Group
		Similar stuff goes together
	Separate
	Differentiate
Don't defy user expectations (ex: link description doesn't match where it goes) - it makes them mad.
Reduce barriers:
	Allow quick account creation and signon.
		Pict.com lets you upload pictures even before you create an account.
	Don't require framework (Flash, Javascript, Silverlight) to be enabled/installed, at least not right away.
	Try to anticipate problems.
		Phone number validation - for God's sake, don't use 3 separate fields!
Affordances:
	Increase text size.
	Make form fields bigger.
	Add label tags that move cursor to field when clicked.
Give feedback:
	Make it clear and obvious that your app is responding appropriately.
	If validation fails, mark the fields with problems directly (indicator *right* next to them).
	Anticipate actions:
		Really cool - validate fields (in Javascript?) even before user submits form.
Simplify:
	"Every time you provide an option, you're asking the user to make a decision."  Avoid it where possible.
	Principles:
		Reduce
			How many elements can you take out of the signup form?
				Get rid of COPPA age validation.
				Tumblr got it down to 2 - username and password.
		Replace
		Hide
			Hide things that can't be acted on right now.
		Remove
			Remove info that isn't necessary.
Use terminology user is comfortable with: it's "delete", not "destroy".
</pre>
