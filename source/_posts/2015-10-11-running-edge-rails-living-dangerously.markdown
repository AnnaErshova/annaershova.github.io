---
layout: post
title: "Running edge Rails -- Living Dangerously"
date: 2015-10-11 18:43:11 -0400
comments: true
categories: Flatiron School, rails, edge rails
---

Rails is constantly being updated and improved. Sometimes, the changes that have been announced are just too exciting to wait for an official release.

When I first read about ‘Edge Rails’, I was quite confused because it sounded like yet another JS library. Then when I was reading The Rails Way (Amazon [link](http://www.amazon.com/The-Rails-Way-Obie-Fernandez/dp/0321445619) if you have somehow never heard of it), I realized I had been mistaken.

Grammatically speaking, it should be spelled *edge Rails*, as in lowercase *e*. But that is really between you and your text editor. In this context, ‘edge' just means the latest, cutting-edge version of Rails that has not been officially released yet.

Rails 5 looming upon us, but there is no official release date. I gather the best guess is late 2015 — early 2016. It does have some exciting features, such as merging of the rails-api gem / built-in support of the JSON APIs). So what do you do if you want to play around with that and don’t want to wait until the official release?

Ruby -v to see if you are using ruby 2.2.2+  as Rails 5 requires it. Use rvm to make sure you are running a suitable version.

The best instructions to install edge Rails can be found [here](http://www.christopherbloom.com/2015/04/26/setting-up-a-rails-5-app-from-edge/) on Christopher Bloom's blog — they are straightforward and and I used them successfully, so I’d rather send you to the source than to copy-paste them here.

RailsGuides has an [EdgeGuides](http://edgeguides.rubyonrails.org/) section specifically targeting the current master branch of the Rails repo.

Running edge Rails comes at a cost of potentially unstable dependencies. Having said that, it is not *that* unstable. Rails has a very extensive test coverage, which should help prevent regressions.

So do you want to run edge Rails? Probably not, unless you really plan to take advantage of groundbreaking unleashed feature or if you are particularly curious. But it’s nice to know it’s there.