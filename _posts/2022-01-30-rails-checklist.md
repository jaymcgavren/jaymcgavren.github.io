---
layout: post
title: 'The Rails Checklist'
tags: []
type: post
published: false
---

Lately when trying to add new features to a Rails app that runs at scale, I feel paralyzed. There's so many security and performance considerations that I can no longer keep them all in my head. I'm a big fan of _The Checklist Manifesto_ by Atul Gawande, so I'm going to see if that format can help me (and maybe you).

## Database Migrations

Create a separate pull request for the migration.

<details>
<summary>Why?</summary>
Code that depends on database changes that haven't happened yet throws exceptions. And migrations on big tables sometimes have to happen separately from deploys.
</details>

[Generate the migration](https://guides.rubyonrails.org/v7.0/active_record_migrations.html#creating-a-standalone-migration)

<details>
<summary>Example</summary>

<code>bin/rails generate migration AddPartNumberToProducts part_number:integer:index</code>

</details>
