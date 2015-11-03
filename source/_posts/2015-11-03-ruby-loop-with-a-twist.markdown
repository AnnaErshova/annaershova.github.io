---
layout: post
title: "Ruby Loop -- With A Twist"
date: 2015-11-03 07:40:33 -0500
comments: true
categories: loop, ruby
---

======
**Decrementing loop:**

Let's start with a siimple decrementing loop in ruby:

{% img center /images/loop_1.png %}

This produces all integers from 100 to 1, each on a separate line:

{% img center /images/loop_1_output.png %}

To produce a slightly more legible output that does not crown our terminal, use **`print`** instead of **`puts`**

{% img center /images/loop_2.png %}

Output:

{% img center /images/loop_2_output.png %}

There is also a **`downto`** method:

{% img center /images/loop_3.png %}

My favorite -- that I always conveniently forget about on the spot -- is **`reverse_each`**

{% img center /images/loop_4.png %}

**`reverse_each`** is really a play on the regular  **`each`** method used with a range, with would iterate through a loop in ascending order:

{% img center /images/loop_5.png %}

To go a little bit fancier and with needless amount of work really, populate and array from a range and then iterate over it:
{% img center /images/loop_9.png %}

Let's not forget the **`step`** method:

{% img center /images/loop_4.png %}

======
**Decrementing | incrementing loop:**

What if the task is to have the **`x`** counting *down*, but to have the integers in the output counting up?

There is a very simple mathematical solution to the problem:

{% img center /images/loop_6.png %}

The result is exactly what we are looking for:

{% img center /images/loop_6_output.png %}

(Here I also added a newline so that it does not clash with terminal prompt.)

I thought of this when asked on the spot, but it's not exactly an elegant solution:

{% img center /images/loop_7.png %}

======
**Incrementing counter | decrementing output:**

Easy and more or less creative solution using a previously populated array for a counter that goes up from 1 to 100 and for an output that goes down from 100 to 1:

{% img center /images/loop_10.png %}

Output:

{% img center /images/loop_10_output.png %}