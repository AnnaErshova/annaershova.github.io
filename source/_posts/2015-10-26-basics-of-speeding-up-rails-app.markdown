---
layout: post
title: "Basics of Speeding Up Rails App"
date: 2015-10-26 18:06:22 -0400
comments: true
categories: 
---


This is a 101 post, and I am planning on touching more on the topics below in greater details.

======

There are three main ways to make Rails apps faster:

* Code optimization
* Scaling
* Caching

======

**Scaling:**

Scaling generally refers to making sure an app remains fast when number of users grows quickly.

So you are a startup that built an app that uses Ruby and Ruby-on-Rails. You did not particularily optimize anything because you just wanted that sweet venture capital for your prototype -- or maybe you did not know what you are doing. Then your startup hit it bit despite the odds, and now you have thousands of users coming to use the app everyday. And that's when things slow down.

Pure Ruby is rather slow, compared to, say C, but there are still ways to make things work efficiently, and I will talk about these.

Heroku scales things for you if that is your deployment tool of choice. Other hosting services tend to have similar solutions.

======

**Caching:**

======

**Code optimization:**

This is the most realiable way to make