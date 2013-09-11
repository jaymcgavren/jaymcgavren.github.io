---
layout: post
title: Ruby subtleties
tags: []
published: false
---

I caught myself writing some things that aren't quite technically accurate while working on my Ruby book.  I'm compiling them here in case they're tripping others up, as well.

> Many other methods take blocks, too!

Not quite.  Here's what I changed it to:

> Many other methods use blocks, too!

*Any* method can take a block, but unless it contains a `yield`, the block is silently ignored.