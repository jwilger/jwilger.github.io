---
layout: post
title: "Using Jeweler for Private Gems"
date: 2012-01-25 11:41
comments: true
categories: [programming, ruby]
---

I really like using [Jeweler] [1] to create and manage gems, but its default
behavior is to publish your gem to [rubygems.org] [2] whenever you run `rake
release`. This is great for generally useful libraries that you want to
open-source, but not as great when you want to use gems as shared libraries for
internal use only (whether because the code contains business secrets or just
because it's not something that would be useful to the community at large.)

After a bit of poking around, I figured out how to use Jeweler to manage
your versioning, gemspec and git tagging without pushing the result to
rubygems.org when running the release task. It turns out to be both obvious and
trivial. Just add the following line to the end of your gem project's
`Rakefile`:

```ruby Rakefile
Rake::Task[:release].prerequisites.delete('gemcutter:release')
```

[1]: http://github.com/technicalpickles/jeweler "technicalpickles/jeweler - GitHub"
[2]: http://rubygems.org "RubyGems.org | your community gem host"
