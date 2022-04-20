---
layout: post
title: 'Trying Rails Constraints'
tags: []
type: post
published: false
---

TODO You're adding a new model to your Rails app. You've run your migration but you haven't set up your model or its validations yet. You'll write specs to test your validations are working, but what about your database constraints? Validations will conceal any flaws in those. Now is a good time to test your constraints.


```
class CreateEmailAddresses < ActiveRecord::Migration[5.1]
  def change
    create_table :email_addresses, id: :bigserial do |t|
      t.bigint :contact_id, foreign_key: true
      t.string :address, null: false

      t.timestamps
    end
    add_index :email_addresses, [:contact_id, :address], unique: true
  end
end
```


``` text
$ bin/rails db:migrate
== 20220420061315 CreateEmailAddresses: migrating ==============================
-- create_table(:email_addresses, {:id=>:bigserial})
   -> 0.0325s
-- add_index(:email_addresses, [:contact_id, :address], {:unique=>true})
   -> 0.0044s
== 20220420061315 CreateEmailAddresses: migrated (0.0371s) =====================

$ bin/rails c
[1] pry(main)> EmailAddress.create()
   (0.5ms)  BEGIN /*application:MyRolodex*/
  SQL (4.6ms)  INSERT INTO "email_addresses" ("created_at", "updated_at") VALUES ('2022-04-20 06:49:30.169899', '2022-04-20 06:49:30.169899') RETURNING "id" /*application:MyRolodex*/
   (0.4ms)  ROLLBACK /*application:MyRolodex*/
ActiveRecord::NotNullViolation: PG::NotNullViolation: ERROR:  null value in column "address" violates not-null constraint
DETAIL:  Failing row contains (1, null, null, null, null, null, 2022-04-20 06:49:30.169899, 2022-04-20 06:49:30.169899).
: INSERT INTO "email_addresses" ("created_at", "updated_at") VALUES ('2022-04-20 06:49:30.169899', '2022-04-20 06:49:30.169899') RETURNING "id" /*application:MyRolodex*/
from /Users/jay/.gem/ruby/2.4.9/gems/activerecord-5.1.7/lib/active_record/connection_adapters/postgresql_adapter.rb:624:in `async_exec'
Caused by PG::NotNullViolation: ERROR:  null value in column "address" violates not-null constraint
DETAIL:  Failing row contains (1, null, null, null, null, null, 2022-04-20 06:49:30.169899, 2022-04-20 06:49:30.169899).

from /Users/jay/.gem/ruby/2.4.9/gems/activerecord-5.1.7/lib/active_record/connection_adapters/postgresql_adapter.rb:624:in `async_exec'
[4] pry(main)> EmailAddress.create(address: "foo@bar.com")
   (0.4ms)  BEGIN /*application:MyRolodex*/
  SQL (2.0ms)  INSERT INTO "email_addresses" ("address", "created_at", "updated_at") VALUES ('foo@bar.com', '2022-04-20 06:52:15.881601', '2022-04-20 06:52:15.881601') RETURNING "id" /*application:MyRolodex*/
   (0.5ms)  COMMIT /*application:MyRolodex*/
=> #<EmailAddress:0x00007fc68b2da6a0
 id: 4,
 contact_id: nil,
 address: "foo@bar.com",
 created_at: Wed, 20 Apr 2022 06:52:15 UTC +00:00,
 updated_at: Wed, 20 Apr 2022 06:52:15 UTC +00:00>
[6] pry(main)> EmailAddress.first.destroy
  EmailAddress Load (0.8ms)  SELECT  "email_addresses".* FROM "email_addresses" ORDER BY "email_addresses"."id" ASC LIMIT 1 /*application:MyRolodex*/
   (0.4ms)  BEGIN /*application:MyRolodex*/
  SQL (0.6ms)  DELETE FROM "email_addresses" WHERE "email_addresses"."id" = 4 /*application:MyRolodex*/
   (0.8ms)  COMMIT /*application:MyRolodex*/
=> #<EmailAddress:0x00007fc68a6d20d8
 id: 4,
 contact_id: nil,
 address: "foo@bar.com",
 created_at: Wed, 20 Apr 2022 06:52:15 UTC +00:00,
 updated_at: Wed, 20 Apr 2022 06:52:15 UTC +00:00>
[7] pry(main)> exit
$ bin/rails db:rollback
== 20220420061315 CreateEmailAddresses: reverting ==============================
-- remove_index(:email_addresses, {:column=>[:contact_id, :address]})
   -> 0.0169s
-- drop_table(:email_addresses, {:id=>:bigserial})
   -> 0.0044s
== 20220420061315 CreateEmailAddresses: reverted (0.0260s) =====================
```

Add `null: false` on the end:

```
      t.bigint :contact_id, foreign_key: true, null: false
```

Then re-run your updated migration:

```
$ bin/rails db:migrate
-- execute("SET LOCAL lock_timeout = '5s'")
   -> 0.0006s
== 20220420061315 CreateEmailAddresses: migrating ==============================
-- create_table(:email_addresses, {:id=>:bigserial})
   -> 0.0089s
-- add_index(:email_addresses, [:contact_id, :address], {:unique=>true})
   -> 0.0030s
== 20220420061315 CreateEmailAddresses: migrated (0.0121s) =====================
```

Now let's try again to make sure a record without a `contact_id` gets rejected by the database:

```
$ bin/rails c
[1] pry(main)> EmailAddress.create(address: "foo@bar.com")
   (0.5ms)  BEGIN /*application:MyRolodex*/
  SQL (2.4ms)  INSERT INTO "email_addresses" ("address", "created_at", "updated_at") VALUES ('foo@bar.com', '2022-04-20 07:00:36.632905', '2022-04-20 07:00:36.632905') RETURNING "id" /*application:MyRolodex*/
   (0.4ms)  ROLLBACK /*application:MyRolodex*/
ActiveRecord::NotNullViolation: PG::NotNullViolation: ERROR:  null value in column "contact_id" violates not-null constraint
DETAIL:  Failing row contains (1, null, foo@bar.com, 2022-04-20 07:00:36.632905, 2022-04-20 07:00:36.632905).
: INSERT INTO "email_addresses" ("address", "created_at", "updated_at") VALUES ('foo@bar.com', '2022-04-20 07:00:36.632905', '2022-04-20 07:00:36.632905') RETURNING "id" /*application:MyRolodex*/
from /Users/jay/.gem/ruby/2.4.9/gems/activerecord-5.1.7/lib/active_record/connection_adapters/postgresql_adapter.rb:624:in `async_exec'
Caused by PG::NotNullViolation: ERROR:  null value in column "contact_id" violates not-null constraint
DETAIL:  Failing row contains (1, null, foo@bar.com, 2022-04-20 07:00:36.632905, 2022-04-20 07:00:36.632905).

from /Users/jay/.gem/ruby/2.4.9/gems/activerecord-5.1.7/lib/active_record/connection_adapters/postgresql_adapter.rb:624:in `async_exec'
```

Let's give it a `contact_id` and make sure it's accepted:

```
[2] pry(main)> EmailAddress.create(contact_id: 1, address: "foo@bar.com")
   (0.5ms)  BEGIN /*application:MyRolodex*/
  SQL (2.0ms)  INSERT INTO "email_addresses" ("contact_id", "address", "created_at", "updated_at") VALUES (1, 'foo@bar.com', '2022-04-20 07:01:06.513430', '2022-04-20 07:01:06.513430') RETURNING "id" /*application:MyRolodex*/
   (0.8ms)  COMMIT /*application:MyRolodex*/
=> #<EmailAddress:0x00007fc68b1c0440
 id: 2,
 contact_id: 1,
 address: "foo@bar.com",
 created_at: Wed, 20 Apr 2022 07:01:06 UTC +00:00,
 updated_at: Wed, 20 Apr 2022 07:01:06 UTC +00:00>
```

One last thing; let's try creating another record with the same `contact_id` and `address`. We _want_ this to be rejected since the address is not unique for this contact.

```
[3] pry(main)> EmailAddress.create(contact_id: 1, address: "foo@bar.com")
   (0.6ms)  BEGIN /*application:MyRolodex*/
  SQL (2.2ms)  INSERT INTO "email_addresses" ("contact_id", "address", "created_at", "updated_at") VALUES (1, 'foo@bar.com', '2022-04-20 07:01:19.978931', '2022-04-20 07:01:19.978931') RETURNING "id" /*application:MyRolodex*/
   (0.5ms)  ROLLBACK /*application:MyRolodex*/
ActiveRecord::RecordNotUnique: PG::UniqueViolation: ERROR:  duplicate key value violates unique constraint "index_email_addresses_on_contact_id_and_address"
DETAIL:  Key (contact_id, address)=(1, foo@bar.com) already exists.
: INSERT INTO "email_addresses" ("contact_id", "address", "created_at", "updated_at") VALUES (1, 'foo@bar.com', '2022-04-20 07:01:19.978931', '2022-04-20 07:01:19.978931') RETURNING "id" /*application:MyRolodex*/
from /Users/jay/.gem/ruby/2.4.9/gems/activerecord-5.1.7/lib/active_record/connection_adapters/postgresql_adapter.rb:624:in `async_exec'
Caused by PG::UniqueViolation: ERROR:  duplicate key value violates unique constraint "index_email_addresses_on_contact_id_and_address"
DETAIL:  Key (contact_id, address)=(1, foo@bar.com) already exists.

from /Users/jay/.gem/ruby/2.4.9/gems/activerecord-5.1.7/lib/active_record/connection_adapters/postgresql_adapter.rb:624:in `async_exec'
```

TODO summarize
