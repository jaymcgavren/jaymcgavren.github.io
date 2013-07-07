---
layout: post
title: Notes from Jim Weirich - Building Blocks of Modularity...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '999'
  original_post_id: '1183'
  _wp_old_slug: '1183'
---
<em>Update 2009-05-05</em>: Saw this talk again today at RailsConf and had a chance to fill in some missing pieces...


<pre>
Is there a grand unified theory of software development?
Principles:
	SOLID
	Law of Demeter
		Method chains not good - only talk to objects in local environment.
	DRY
	Small Methods
	Design by Contract
Myer on Coupling: old, imperfect model that doesn't extend well to dynamic languages.  From best to worst:
	No coupling
	Data coupling
		Data local to two modules: simple data
	Stamp coupling
		Data local to two modules: structured data
	Control coupling
		Method usually has a "flag" parameter that controls which algorithm it uses
			ex: Array.instance_methods(true) #What does true mean?!
			ActiveRecord#find (:first, :all, etc.)
	External coupling
		Global data: simple data
	Common coupling
		Global data: structured data
	Content coupling
Connascence
	Things that are born together, and change together.  A change in one requires a corresponding change in the other.
	Originally applied to software by Meilir Page-Jones in early 90's.
Connascence of Name:
	class Customer
		def email; blah; end
	end
	def send_mail(customer)
		customer.email #Change Customer#email's name, you must update this call.
	end
Rule of Locality:
	Connascence of name between method parameter and a reference in the same method doesn't matter at all.
	Connascence of name between two separate libraries matters a lot.  It's why APIs must be frozen.
Connascence of Position:
	:orders =&gt; {"3" =&gt; "1", "5" =&gt; "2"}
	[ [ Order.find(3), true], [ Order.find(5), false ] ]
	Order of parameters decides behavior.
	Really bad:
		def process(order, expedite, confirmation_number, ...); blah; end
		[order, true, 2374]
		Easy to forget order of parameters, especially if you're passing 3, '
	Better:
		class OrderDisposition
			attr_reader :order
			attr_reader :expedite
			attr_reader :confirmation_number
		end
	Methods that take hash parameters are better than positional arguments, because each argument is labelled and can be re-ordered or omitted.
Degree matters:
	Some types of connascence are worse than others.
	Connascence of Name better than Connascence of Position.
Rule of Degree:
	Convert higher degrees of connascence into weaker forms.
		Example: refactor from positional method params to an options hash with named keys (CoP -&gt; CoN).
Connascence of Meaning
	Consider "magic numbers" (these are bad):
		&lt;input type="checkbox" value="2"&gt;
		if params[:med][id] == "2" #Have to do case-like statement in totally different module.
			@medication.given = false
		end
Contranascence
	Things conflicting with each other.  (Always in name?)
		#my_xml_lib
		module Kernel; def node; end; end
		#my_graph_lib
		module Kernel; def node; end; end #Conflict!
	Example is classes that must be namespaced to avoid conflict (XML::Node, YAML::Node)
Connascence of Algorithm:
	Logic repeated in multiple places - not DRY.
	Bad:
		def add_check_digit(digits); digits + ((10 - digits.foobar{|d| d + 5} % 10).to_s; end
		def check?(digits) check_sum(digits.foobar{|d| d + 5}) == 10; end
		Change digits.foobar{|d| d + 5} in one place, you must change it in both places.  Better not forget!
	Better:
		def add_check_digit(digits); digits + ((10 - foobar(digits) % 10).to_s; end
		def check?(digits) foobar(digits) == 10; end
		def foobar(digits); blah; end #Shared routine
		Change the shared routine, and you change the logic everywhere you need to.
Connascence of Timing
	Race conditions.
	Bad if called from multiple threads:
		def increment
			@amount += 1
		end
	Use Java-like synchronized declarations on methods to ensure they are thread-safe.
Connascence of Type
	See What Every Programmer Should Know About Object Oriented Design, Meilir Page-Jones
Connascence of Execution
	See What Every Programmer Should Know About Object Oriented Design, Meilir Page-Jones
Connascence of Value
	See What Every Programmer Should Know About Object Oriented Design, Meilir Page-Jones
Connascence of Identity
	See What Every Programmer Should Know About Object Oriented Design, Meilir Page-Jones

</pre>
