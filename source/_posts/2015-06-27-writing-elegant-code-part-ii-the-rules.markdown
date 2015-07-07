---
layout: post
title: "Writing Elegant Code Part II: The Rules"
date: 2015-06-27 20:22:39 -0400
comments: true
categories: Flatiron School
---

I remember curiously peeking at code on GitHub before starting Flatiron. Even then, despite not understanding all too well what the code was meant to do, I could tell that some of it was easier to read than others. My favorite samples had methods that were short and clearly named, variables has clear names, code was organized logically and everything was properly indented.

Now that I can (mostly) write some functioning code, it is time to make sure it is easy to understand to those who may read it at a later point.

And so I went in search of re-factoring rules -- and I found them.

The Rules are Sandi Metz' Rules for Developers and are discussed [here](https://robots.thoughtbot.com/sandi-metz-rules-for-developers).

I am paraphrasing them slightly below:

> 1. Classes can be no longer than 100 lines of code ( # sloc -- we are not counting blank lines) to ensure they stay within the single responsibility principle for classes.

> 2. Methods can be no longer than five lines of code in Ruby proper (Rails is hard, and I am still not sure how it is meant to work). And yes, if statements with else and elfish count. Don't do them. Break your code into reasonable methods with easy-to-follow names [use neonates as an example]. 

> 3. Pass no more than four parameters into a method. Hash options are parameters, too.

> 4. Controllers can instantiate only one object. Views can only know about one instance variable; views should only send messages to that particular object.

I will touch on all of these later,  but in this post, I wanted to discuss applying the first 2 in real life (insofar as solving labs can count as 'real life', of course).

For a lab this week, we had to write a simple game of Rock Paper Scissors and then turn it into a simple web app using Sinatra. To create such a game is far from challenging, and my code was already reasonably succinct at the point when I got all the rspec tests to pass. (NB: that is not how I would actually write the game, but it worked in a lab context). 

But the code still felt it could use some re-factoring:

{% img center /images/RPpre-refactoring.png %}

Enter The Rules.

My class was much shorter than the mandated 100 lines of code -- check. 

Most of my methods were one-liners with 3 winning scenario helper methods designed to not clutter my  won? method. So far, so good.

But what is going on lines 33 to 41? (that method is called on in app.rb to integrate into Sinatra.) 

{% img center /images/outcome.png %}

It felt too simplistic -- just an if-then statement? really? And I was just itching to improve it somehow. It certthe explicitly frowned upon elsif was there!). 

I was not entirely sure how to improve it other than via a nested ternary operator. While I like ternary operators as much as the next noob Ruby developer who thinks they are really cool-looking, nesting them is just the opposite of my goal of writing code that is easily understood by others. 

{% img center /images/nestedternary.png %}

I had a very vague notion of experimenting with something else instead: calling on all 3 methods, checking which one returns true (and in this case, one and only one will return true) and then returning interpolated name of that method with an exclamation point instead of a question mark. So if method won? is the one that returns true, then the game response would be 'you won!'

I went to one of the instructors, Sophie, seeking her counsel on how to execute just that. After some pry-ing around, we have decided that such a solution would not actually save me any lines of code, because I woulf have to write new methods that will take up the very lines I have saved. 

But Sophie did point out something the test did not cover: the computer_play method was sampling the USER_CHOICES (previosuly known as VALID_MOVES) array every time, so I needed to assign it to an instance variable (and that is why pair programming with a more senior professional is so important).

Upon some consideration, I also got rid of the winning scenarios methods (3 basically identicaly methods? sounds like something in need of abtraction to me) by creating a VICTORY_HASH constant. 
{% img center /images/victory_hash.png %}

At that point, I could have gotten rid of the VALID_MOVES array, reading it as keys or values of VICTORY_HASH instead, but to keep it allows for better code comprehension, so it was spared from culling.

{% img center /images/valid_moves.png %}

To make everything orderly, I re-named 'user_move' as 'user_play', because I wanted its name to be symmetrical to the computer_play method (whose name was in turn mandated by Rspec).

{% img center /images/user_move.png %}
{% img center /images/user_play.png %}

The final code ended up being shorter than before by around 10 lines:

{% img center /images/refactored_rps.png %}

And the 'outcome' method? It is still there, staring at me in its simple flow control glory. Rules exist to be broken, I suppose. 