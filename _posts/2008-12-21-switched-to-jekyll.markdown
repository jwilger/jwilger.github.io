---
layout: post
title: Switched to Jekyll
date: 2008-12-21
comments: true
categories: meta
---

If you're seeing this, then you see that I've stopped hosting my blog on Blogger
and am now using a slightly modified Jekyll. Jekyll is the engine that powers
GitHub's recently announced "pages" feature.

I'm not hosting on GitHub, though. I simply installed Jekyll on the cheapest VPS
from Slicehost, set up a git repository on that server to hold the contents of
the site and then slapped together a simple post-update hook script for git that
automatically publishes the site when I commit changes.

The changes also come with a new design.

Dragons are cool, so I am cool.

The stylesheets obviously aren't fleshed out yet, so everything pretty much
looks like crap. I plan to have it fixed up real soon.

Also need to slap together a new Atom feed for the posts.

All worth it, since I can now easily compose my posts in Vim using markdown
syntax and have them stay editable in that format. Maybe now I'll actually post
more than once every couple of months. :-)
