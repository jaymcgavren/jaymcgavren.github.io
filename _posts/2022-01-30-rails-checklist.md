---
layout: post
title: 'The Rails Checklist'
tags: []
type: post
published: false
---

Lately when trying to add new features to a Rails app that runs at scale, I feel paralyzed. There's so many security and performance considerations that I can no longer keep them all in my head. I'm a big fan of _The Checklist Manifesto_ by Atul Gawande, so I'm going to see if that format can help me (and maybe you).


## Planning

- Run database queries and do other research to determine the following:
    - Full range of input values your code can receive.
    - Throughput your code must handle under peak load.

If you're fixing a bug:

- Gather a set of inputs that will reproduce the bug. Save them to use in a test, whether manual or automated or both, after you've coded a fix.


## Database Migrations

Create a separate pull request for the migration.

<details>
<summary>Why?</summary>
Code that depends on database changes that haven't happened yet throws exceptions. And slow migrations on big tables often have to happen separately from deploys.
</details>

[Generate the migration](https://guides.rubyonrails.org/v7.0/active_record_migrations.html#creating-a-standalone-migration)

<details>
<summary>Example</summary>

<code>bin/rails generate migration AddPartNumberToProducts part_number:integer:index</code>

</details>

Deploy and run the migration. See [Deployment](#Deployment).

## Models

### Database

Are you using transactions where you should be?

<details>
<summary>Why?</summary>
Does your code make a series of database updates? Will your app be in an inconsistent state if only some of those updates occur?
</details>

Can your transactions run too long?

<details>
<summary>Why?</summary>
Transactions acquire locks on all the records they're updating, which can result in [deadlocks](https://vimeo.com/12941188) under load.
</details>


### Validations

For enum and enum-like attributes, are there valid values you're not allowing?


## Controllers



## Metrics/Logging

What exceptions could your code possibly throw? Can you differentiate your exceptions from others of the same type? Will you be alerted if they occur too frequently?

The app metrics or logs should record the time lengthy operations take to complete.

In the event an operation fails, the logs should contain the operation parameters to aid in troubleshooting.


## Code Review

Review the diff of your PR. What app features could break, and in what ways?

Use your above analysis to test your own code. As you test, write up directions that will help QA or other devs to test as well.


## Merging

Review your PR again and check your deployment plan.

- Ensure any ENV variables will be set not just in production, but also staging and any other environments that need to match production.
- Ensure feature flags will be set appropriately.
- Update your monitoring app:
    - With any metrics/logging added to the code.
    - Add queue size, run duration, and success/failure status for any background jobs to dashboards.
    - Add queue latency and job failure alerts with appropriate thresholds.


## Deployment

Following a deployment:

- Check the application error reporting or logs for the following:
    - New exceptions never seen before.
    - Post-deploy occurrences of known exceptions. Could they have been caused by your deploy?
