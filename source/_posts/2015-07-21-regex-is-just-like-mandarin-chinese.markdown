---
layout: post
title: "RegEx Is Just Like Mandarin Chinese"
date: 2015-07-21 08:26:33 -0400
comments: true
categories: Flatiron School
---

When I was in primary school in Russia, we had an intro to computer science class that taught up the basics of programming to produce good post-Communist STEM-oriented comrades. It used Basic to teach the fundamentals. As I spoke no English at the time, I spent more time memorizing words like GOTO and GOSUB than actually figuring out coding logic.

English speakers have a very distinct advantage when it comes to programming in most languages: we know all the words already. One doesn't even have to be an actual native speaker: Ruby was famously written by a Japanese programmer.

Whether a native speaker or not, it is a lot easier to memorize certain methods in Ruby (see: any?; none?; all?) when one actually understands how to use those words in a sentence.

Learning to code is comparable to learning a foreign language: a large part of it is comprehending the principles and then complementing it with memorizing quirks of grammar.

I compared SQL to German in class before. German is a very structured language where sentences have to be built and organized a very certain way, just like SQL. 

Compare that to an Eastern European language, where we take major liberties with positioning words in a sentence. I used to tutor Russian as an undergrad at Yale; I remember students coming to me panicking because they could not figure out why subjects and objects were creatively arranged in a sentence and what to do about it. All I could say at the time is they were lucky because they did not learn Ukrainian, which has same creativity, by more complex grammar.

Ruby feels like an Eastern European language to me -- there are many ways to write code, but there are still very specific 'grammar' rules one needs to follow to make code 'grammatically correct.' The stakes of course are differnet: while one can make oneself understood and convery the message well in broken Russian, Ruby won't run broken code at all or run it incorrectly.

Here is the problem with RegEx: it is just like Mandarin Chinese. Judging by the number of desperate, hate-filled posts on StackOverflow, it is as hard to learn.

Mandarin Chinese, and most its other dialects of Chinese actually have no well-developed grammar. There are ways to structure sentences, but there are no 7 cases of Ukrainian or 12 tenses of English. Past tense is barely denoted, yet alone formed in a miriad ways that hapless students of Germanic languages spend years memorizing. 

When I first started Ruby, I routinely had to spend a fair bit of time ensuring I had an appropriate number of 'end' key words: one to end an if statement, one to end a do block, one to end a method, one to end a class... That's a lot of 'grammar' to learn -- but at least we all know what the word 'end' means, so that makes it easier. With RegEx, you have to poke around various seemingly randomly assigned symbols and hope that they work. Just like with Mandarin, half the time you are hoping you are refering to the correct character that has no real linguistic content and that you are using it correctly.

For a project in class, I had to write the following expression to validate a potential twitter handle: /^[A-Za-z0-9_]{1,15}|^@[A-Za-z0-9_]{1,15}/. It's not technically that difficult, but who decided that ^ stands for start of line? Or that $, for that matter, stands for end of line? Or that 'a?'' means zero or more of soemthing? 

There might be some internal logic to it, just like with Chinese (vestiges of old-school computer science perhaps?), but for a modern-day person without much linguistic...I mean computer science background, it is not intuitive.

On top of that, to use RegEx is like writing an application without a good test suite: you think that you have thought of everything, but there is always that one edge case that can pop up and screw it over. I felt like that when learning Mandarin: something always pops up where the word has a diferent meaning or is really meant to be used with a different character to really 'work.'

The good news is that both RegEx and Mandarin are possible to master. Perseverance and a healthy amount of grunt work is key. But just like Mandarin is handy for freaking out Chinese restaurant employees and nail salon workers, RegEx is handy too -- in fact, it might have a greater utility of being used oftenf or the rest of one's Web Development career.