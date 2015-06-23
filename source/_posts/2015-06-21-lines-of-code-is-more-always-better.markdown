---
layout: post
title: "Lines of Code: Is More Always Better?"
date: 2015-06-21 11:24:04 -0400
comments: true
categories: Flatiron School
---


A book on Ruby I have been reading brought up an interesting fact: it is common for programmers to be evaluated based on how many lines of code (a.k.a. source lines of code, SLOC) they write per unit of time. 

I see how that is commonly applied in a corporate environment. Everyone needs to be evaluated on something. Traders are evaluated on their profit-and-loss statements. Teachers are evaluated on their students' standardized test performance. My cat is evaluated on his cuteness. 

So programmers also should be evaluated based on something they do day in and out: writing code. And the more they write, the better their performance is. Right?

It seems to be a no-brainer: if you write a lot of code, surely you are very productive and, by extension, also a very capable programmer. 

Furthermore, if you wrote 1,000 lines a week on average for the past few weeks, and your colleague wrote only 500 lines while working in the same language -- you work much harder and your colleague is not pulling her weight. Right?

It's not all as clear-cut.

There is no doubt that complex programs require a lot of lines of code. A cursory [internet search](http://www.quora.com/How-many-lines-of-code-does-Windows-7-have) suggests Windows 7 has 2,085,772 lines of code, although I am sure that can be much improved upon if re-written from scratch; but not even the most capable programmer can convert it into 2,000 lines of code.

It is obvious that a program that has several million lines of code is much more complex than that that has several thousands. But for the same complexity level, is it better to have more code?

So far, most of my own Ruby code refactoring -- once I got past the 'Hello, World' stage - involved abbreviating number of lines of code once I got the program to work (outside of maybe using modules, but even then, I probably end up with fewer lines of codes on a net-net basis). 

My current steep learning code means that sometimes I see a new method and realize I should have used that on a lab from a week ago, so I go in and apply it, which usually results in fewer lines of code:

{% img center /images/factorial.png %}

{% img center /images/factorialternary.png %}

{% img center /images/inject.png %}

Why go and create a custom factorial method if one can just use 'inject'?

So to me, a metric of learning performance has been being able to remove code and replace it with something more efficient and elegant that does not take away from the program's performance.

I stumbled upon a relevant E.W. Dijkstra's quote when researching the topic; It was featured in his 1988 paper ['On the Cruelty of Really Teaching Computer Science'](https://www.cs.utexas.edu/~EWD/transcriptions/EWD10xx/EWD1036.html):

> "... [there] is only a small step to measuring "programmer productivity" in terms of "number of lines of code produced per month". This is a very costly measuring unit because it encourages the writing of insipid code [...] 

> My point today is that, if we wish to count lines of code, we should not regard them as "lines produced" but as "lines spent": the current conventional wisdom is so foolish as to book that count on the wrong side of the ledger."

I will leave you with another quote by Bill Gates:

> Measuring programming progress by lines of code is like measuring aircraft building progress by weight.

Don't waste your code -- write it succinctly.

