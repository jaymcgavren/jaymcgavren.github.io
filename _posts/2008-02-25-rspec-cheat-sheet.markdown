---
layout: post
title: rSpec cheat sheet...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '734'
  original_post_id: '786'
  _wp_old_slug: '786'
---
Here's a cheat sheet on rSpec with almost completely raw formatting...  I'll HTMLify it if anyone's interested.

<!--more-->

<pre>
describe X {block} and describe X, ".y" {block}: in {block}, describe the behavior of class X (or its y method)
	it("description") {block}: in {block}, use matchers to define expectations.
	before, before(:each), before(:all): set up before each test or before all tests
Matchers:
	Use .should_not for negatives
	target.should be_x: method x? should return true
	target.should be_close(x, margin): target number should be within margin of x
	target.should be_an_instance_of(X): should be of class X or a subclass
	target.should have(x).y, target.should have_at_least(x).y, target.should have_at_most(x).y: method y should return array of (at least/most) length x
	target.should match(/x/): regexp matching
	target.should raise_error(x): should throw Exception of (optional) type X
	target.should respond_to(x): should respond to message x (auto-converts strings to symbols)
	target.should satisfy {block}: yields target to {block}, passes if {block} returns true
Custom matchers:
	Define a new class with the below methods:
		initialize():
		matches?(target): returns true if target matches, false otherwise
		failure_message: returns "expected x but got y" string to be displayed upon failure
		negative_failure_message: returns "expected x to not be y" string to be displayed upon failure of should_not clause
	Define a method in the current module that instantiates the new class.  This is the method target.should will call.
Mocks:
	.should_receive(:x): test fails if method x is never called
		{block}: can provide {block} and use matchers to set expectations for arguments
		.and_return(y): returns value y when mock method is called
		.and_raise(y): raises exception y when called
		.and_yield(values): yields values when called
			.and_yield clauses can be chained to yield different values on subsequent call
		.with(x, y): test fails if method is never called with arguments x and y
			Can use these in place of specific arguments:
				:no_args
				:any_args
				:numeric, :boolean, :string
				/pattern/
				:anything
				ducktype(:x, :y): argument should respond to x and y
		Method call counts:
			.once, .twice, .exactly(n).times
			.at_least(n).times
			.at_most(n).times
			.any_number_of_times
		.ordered: method will be added to list of methods expected to be called in order
	.stub!(:x): like should_recieve, but does not fail if never called
User Stories:
	Plain text format:
		Begins with "Story: [title]"
		Business case:
			As a [role]: Who user is (user, admin, etc.)
			I want to [perform action]: login, set permissions, etc.
			So that [business value]: "I can get access to the site", "I can sell my goods", etc.
		Scenarios:
			Begin with "Scenario: [description]"
			'Given' clauses: set up for use case
				Given a user 'jdoe'
				And a document 'noname.txt'
			'When' clauses: show action
				When the user is logged in
				And the user reads the file
			'Then' clauses: show expectations
				Then the file's contents should be returned
	Story steps:
		steps_for(:category) {block}: Define given, when, and then blocks within {block}
			Given "string with match $marker(s)" {|marker| block}
				Matches 'Given' clauses in plain-text story (or And clauses that follow Given)
				Word in plain-text story that matches $marker will be passed to {block}
				Can also use regexp with capture groups in place of match string
				Within {block}, use rSpec or other Ruby code to set up for test
			When "string with match $marker(s)" {|marker| block}
				Same as Given, but matches When (or subsequent And) clauses
				Within {block}, perform actions
			Then "string with match $marker(s)" {|marker| block}
				Same as Given, but matches Then (or subsequent And) clauses
				Within {block}, define expectations
	with_steps_for(:category) {block}
		Reference :category set up by earlier steps_for() call.
		run(text_file, options): Run plain text story in text_file with given steps
</pre>
