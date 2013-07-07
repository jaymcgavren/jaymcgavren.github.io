---
layout: post
title: 'Notes from RailsConf - Rails 3: Step Off the Golden Path...'
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1012'
  original_post_id: '1202'
  _wp_old_slug: '1202'
---
Hosted by Matt Aimonetti.

<pre>
Rails philosophy:
	Convention over configuration
Merb philosophy:
	Performance
	Framework agnosticism
Rails 3 philosophy is also a merger:
	Performance
	Modularity
	Framework agnosticism
What you get:
	Public API (It was closed for Rails 2)
	Mountable apps (mount your blog app in your CMS app)
Default stack:
	ActiveRecord
	Test::Unit
	Prototype
	ERB
But, it's less opinionated:
	Other Javascript frameworks:
		jQuery
		MooTools
		ExtJS
		Yahoo!
	Other templating engines:
		Haml
	Other ORMs (turn DB records into objects):
		DataMapper
		Sequel
		CouchRest
	Other test frameworks:
		Cucumber
		RSpec
When to step off the golden path:
	If your templating, JS, ORM, or performance requirements differ.
	Otherwise, use the default stack- it's real-world tested.
Datamapper:
	Procrastination as a virtue:
		Lazy Loading - Don't pull fields until they're asked for specifically.
		Strategic Eager Loader
		ActiveRecord:
			Student.all.each.books.map {|b| b.name}
			select * from "students"
			select * from books where student_id = "1"
			select * from books where student_id = "2" #etc. This is slow!
		DataMapper:
			Student.all.each.books.map {|b| b.name}
			select id, name from students order by id
			select id, name, student_id from books where
				(student_id in (1, 2, 3, X)) order by id --Faster
	Multiple "repos" (databases)
		Config:
			production:
				adapter: mysql
				database: production-app
				host: localhost
				...
			repositories:
				nightly_backup:
					adapter: sqlite3
					database: shared/nightly.db
				weekly_backup:
					...
		Then set up a task to copy from DB to repo:
			Article.copy(:default, :nightly_backup, :created.gt =&gt; 1.day.ago)
		Legacy databases:
			class Page
				include DataMapper::Resource
				property :id, Serial
				property :name, String
				#Specify different fields when talking to legacy database:
				repository(:legacy) do
					property :name, String, :field =&gt; "title"
				end
			end
	Query::Path
		#Joins people with addresses, finds records where street column LIKE '%street%'
		Person.all("addresses.street.like" =&gt; "%street%")
	Many adapters:
		RDBMS
		file system
		IMAP
		YAML
		SalesForce
		REST APIs
		your API here - write your own.
Sequel
	High performance
	Sharding
	Prepared statements
	Highly customizable SQL statements
Hibernate
	Built in sharding
	ActionORM
	JRuby
	Many Java libraries for legacy databases
Non-RDBMS systems
	AppEngine::DataStore
	CouchRest for CouchDB
	Redis, Tokyo Cabinet, etc...
More customizations available:
	File structure (including very_flat)
	Custom router DSL
	Custom request handlers
		class Presentation &lt; ActionController::Http
			def index
				self.response_body = "Hello!"
			end
		end
		Presentation.action(:index).call(Rack::MockRequest.env_for("/railsconf"))
</pre>
