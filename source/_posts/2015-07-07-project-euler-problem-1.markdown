---
layout: post
title: "Project Euler Problem 1, or Benchmarking Ruby Code"
date: 2015-07-07 05:56:19 -0400
comments: true
categories: Flatiron School, Project Euler
---

Everyone loves a good coding challenge. But where do you find good brainteasers outside of StackOverflow's endless Ruby 101 questions?

Enter [Project Euler](https://projecteuler.net/). At 513 problems and counting, it is a great way to practice both your math and coding skills.

Many of the initial problems are on the easier side, and when I was assigned [Problem 1](https://projecteuler.net/problem=1), it did not take long to figure out how to approach solving it:

> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

> Find the sum of all the multiples of 3 or 5 below 1000.

We were supposed to code both a 'regular' procedural and an object-oriented solution.

Here is a very quickly written procedural one in a lab context (the two methods used and their names came from rspec suite):

{% img center /images/pe1procedural.png %}

It's pretty straightforward. There is a simple loop to find all the multiples of 3 or 5 and push them into an array; inject method is then used to sum up all of them (yes, one can iterate over the array instead, but inject is perfect for summing or multiplying array contents, so I was not going to bother).

It works perfectly fine -- the answer is 233168, by the way.

But then I got thinking: there are just *too many lines of code*, and writing them is not exactly efficient. I create an empty array; I create a variable with initial value of 3 (or 1, but our common sense tells us we don't need 1 and 2 anyway), I increment by 1; I push things into the array. It just feels like too much effort.

So for the 'object-oriented solution', I made things a little more elegant:

{% img center /images/pe1oo.png %}

That is easier to read and it just *looks* a lot better, and it produces the same result. But ultimately, it is not enough for code to be handsome, it also has to be fast and efficient. It was a good chance to use Ruby's [Benchmark Module](http://ruby-doc.org/stdlib-1.9.3/libdoc/benchmark/rdoc/Benchmark.html) to see if one solution was preferable to another due to it being faster.

Quoting straight from the source:

>The Benchmark module provides methods to measure and report the time used to execute Ruby code.

It is pretty straightforward. One has to 'require 'Benchmark' and then use Benchmark.measure { *whatever expression one is evaluating* } -- use 'puts' to see the actual outcome.

My initial plan was to benchmark my 'longer' loop solution vs. select vs. a similarly-coded reject solution, vs. several conditions ( using || for modulo or using min) and see if one was preferable to another.

So I ran benchmark on the select statement. And then I ran it again on the same statement. And again. And the processing times were different. And again -- still different. Here is what it ended up looking like:

{% img center /images/benchmarkselectcomparison.png %}

The time on the right is 'elapsed real time', which is basically time it took the program to run from beginning to and end.

Since the unit of time in which the output is shown is seconds, the amount of time it takes to execute is very small. In the 14 examples above, we are talking the slowest example taking just above a millisecond.

But I expected running the *same* line of code to take the *same* time each and every time. After all, there are no random number generators in that code, and Ruby should evaluate the line of code in the same order each time -- the result doesn't change, why would processing time?

What's interesting about Benchmark is that it is affected by CPU, and your CPU will be running differently every time you run Benchmark. Although it took me several seconds before benchmarking attempts in the example above, and I did not start of exit any new software (or Chrome Tabs) in between attempts, my CPU clearly was doing different things at the time, hence the time variations.

So how is one supposed to benchmark one process against another if it is also affected by 'outside' factors such as whatever else your computer is doing in the background? The trick is to run your line of code against the other ones multiple times simultaneously, and then average processing times.

There is a very handy solution suggested in the documentation, which I have used to run 5 different statements 100 times and then evaluate results:

{% img center /images/benchmarkingcode.png %}

Here is the outcome, run within 3 seconds of each other:

{% img center /images/benchmarkingcomparison.png %}

While the absolute numbers are different each time benchmarking is run, the relative numbers remain the same (I ran it a few more dozen times and charted it, but I won't bore you with the details).

The fastests solutions were using logical operators vs. applying min<1 -- the latter took at least 2.5x longer than the 3 solutions that used Boolean operators -- can you guess why? 

However -- all of the evaluted solutions took well under a second, so it is not really significant for this particular problem. But speed is a major concern for many industries (see a very interesting NYTimes article that discusses how it applies in finance ([article here -- paywall](http://www.nytimes.com/2014/04/14/opinion/krugman-three-expensive-milliseconds.html?_r=0))).

Certain companies employ entire teams of people whose job description is to shave off milliseconds of algorithm running times. While Ruby's Benchmarking module is not powerful enough for those commercial purposes, it is a fun way to experiment with the code one writes to see how it compares against other options.

