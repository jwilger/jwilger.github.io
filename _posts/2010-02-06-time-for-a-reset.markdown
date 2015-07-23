---
layout: post
title: Time for a Reset
date: 2010-02-06
comments: true
categories: meta
---

Hello, World! (?)

I've had the decision to completely restart my website made for me. The
previous incarnation of my site was being generated via a post-commit hook in
a git repository that lived on a VM at Slicehost. I decided to shut down that
VM and move the website to a system that I didn't have to maintain.
Unfortunately, I *thought* that I had the git repository mirrored on [my
GitHub account](http://github.com/jwilger), but apparently not.  I'm sure I
could come up with usable backups if I put forth enough effort, but let's be
honest: thanks largely to [Twitter](http://twitter.com/jwilger), I had barely
updated the site in the last 2 years, and a lot of what was there was either
outdated or of no real value to anyone other than myself.

So here we go again. <strike>This time around, I'm just using [GitHub's pages
feature](http://pages.github.com) to publish the site. I don't have to
maintain the server, and now I *know* that the repository is on my GitHub
account.</strike>

**UPDATE** I'm actually switching to using
[toto](http://github.com/cloudhead/toto) with [Heroku](http://heroku.com). I
like toto better than jekyll, because I don't have to put up with using the
Liquid page templating engine. Plain-old ERB FTW!
