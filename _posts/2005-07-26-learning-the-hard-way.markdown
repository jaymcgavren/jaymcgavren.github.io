---
layout: post
title: Learning the hard way...
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  original_post_id: '257'
  _wp_old_slug: '257'
---
Over the past two projects, every time I've realized I made a mistake, I've made a note to myself.  ("Lessons Learned", in business jargon.)  Here's a collection.  (Yes, some of these are "well, duh" statements - they're here to document situations that I let business inertia drag me into.)

-Check project management resources for frequently missed items in estimating project timeline.
-Be sure to to document user classes and areas of interface they must be allowed to access/denied access to.
-Release Management/Operations needs to know when daemons actually terminate if they don't die right away.
-Set up one of every type of network connection on localhost for dev (and other environments), so you can test functionality that uses these protocols.
-Structure modules/methods in such a way that they can be easily unit tested!
-Support all options for a protocol in your config files, not just those you initially plan to use.
-Document default values for all configuration options, reasons behind them.
-Ensure systems administration and database administration are on signoff list for technical design, so they can raise security/efficiency issues.
-Never use any unencrypted protocol, even within an intranet; other departments are likely to block it.
-Estimate time up front to build unit/integration test harnesses, builder/installer for all environments.
-Project managers always assume developers will be allocated 100%, when in fact it is more like 80%.
-Note all servers for project and types of connections made by application, then request setup from Systems Administration prior to beginning coding!
-Plan around reloading config before accessing each option, so changes can be made without shutting down.
-Use one config hierarchy for everything, so you don't have to manage multiple files.
-Allocate time for TDD revisions, as other departments review it for the first time.
-Calculate expected load on networks, databases, etc. in advance.
-Ensure vendors fully understand all requirements (and their difficulty) before signing any work agreements.
-Don't accept specifications that are vague or open to interpretation, as requester is likely to reject finished product.
-Write down all figures you give to others in meetings for later reference (such as effort estimates).
-Skimping on code reviews costs almost as much time as it saves, and may result in a lower-quality product.
-Monitoring tools must raise alarm if items in processing queue get too old.
-Manual installation of files not advisable.  Consider making RPM.
-Specify precise file locations and names for each module in technical design.
-Maintain separate config directories for development, testing, production!
-Ensure all generic accounts (FTP, database, etc.) are created well before rollout!
-Specify whether paths will be absolute or relative.
-Use 'set' as a verb in method names rather than 'add', unless you intend it to fail if the value already exists.
-Perl is a poor language for outsourcing.
-Perl is a poor language for building large applications.
