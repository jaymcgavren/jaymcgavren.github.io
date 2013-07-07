---
layout: post
title: Safely running an MIT Scratch class for kids with Mac OS X Parental Controls
tags: []
status: publish
type: post
published: true
meta:
  _publicize_pending: '1'
  ljID: '1022'
  original_post_id: '1217'
  _wp_old_slug: '1217'
---
Or, at least, my attempt at it.  The real-world test is this Saturday; I'd be interested in any further advice anyone can offer.  I'm trying to balance security with ease of setup.  This can of course be adapted to other applications.

<ul>
<li>In the Finder, copy the Scratch folder from the disk image to /Users/Shared/ under the Macintosh HD.</li>
<li>To ensure files can be saved to the Scratch Projects folder (which is the default location for a fresh Scratch install), in Terminal, run "chmod -R ugo+w /Users/Shared/Scratch 1.3.1" (or whatever the Scratch folder path is).</li>
<li>Enable the Guest account via the Accounts preference pane.</li>
<li>In the Parental Controls pane, enable parental controls for the guest account.</li>
<li>Check "Use Simple Finder" (this will make it easier for younger kids to navigate to the app).</li>
<li>Check "Only allow selected applications", and ensure all applications are disabled except Safari (for establishing scratch.mit.edu accounts) and Scratch.  (If the top-level checkbox has a minus-sign, it means some sub-items are enabled.  Click the box until it is empty, then expand the tree view to select individual sub-items.)</li>
<li>Under the Content tab, select "Allow access to only these websites", click the plus sign, and add http://scratch.mit.edu/ to the list of allowed sites.</li>
</ul>

When the machine boots, students should be able to click the Guest account, then select the Shared folder in the Dock to get to the Scratch app.  (I don't know an easy way to add Scratch itself to the Dock under the locked-down Finder; let me know if you do.)  They can also open and save Scratch projects within Scratch itself, and they'll be preserved after logout even though it's a guest account.  Safari access lets them establish an account on scratch.mit.edu so they can upload their projects.

They won't be able to do much of anything else, though - all apps will be hidden, and almost all paths will be inaccessible from the Finder.  (They can still see almost anything from Safari, but next to nothing will be writable.)  I'd imagine this is enough to keep most kids out of of distraction and/or trouble, but you can disable Safari and lock the machine down still further if you're concerned.

<em>Edit</em>: My post on how the class went is <a href="http://jay.mcgavren.com/blog/archives/1219">here</a>.  Summary - I wouldn't say these efforts were unnecessary, but they definitely weren't essential.  We had the program up and running when kids arrived, and that was all we really needed.  Security wasn't much of a concern in this environment.
