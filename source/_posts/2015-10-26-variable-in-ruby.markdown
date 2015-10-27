---
layout: post
title: "Global Variables in Ruby"
date: 2015-10-26 19:02:49 -0400
comments: true
categories: variables, ruby, global variables, constants
---

======

**Variables in Ruby and Their Scope:**

There are four major kinds of variables in Ruby, like in most object-oriented languages:

* **Global** 
* **Local**
* **Instance**
* **Class**

There are also special variables such as **`self`** or **`nil`**, and of course, one can classify constants as a kind of a variable.

In this post, I want to talk about global variables, which, as the name implies, are stored globally and have global implications.

All variables in Ruby outside of locals ones are indicated with a sigil (a prefix that denotes variable scope): **`@`** for instance variables, **`@@`** for class variables, and **`$`** for global variables.

Since Ruby is a dynamically typed language, interpreter will determine data type of each and every variable when it is being assigned; there is no need to define each variable's data type when introducing it (so no need to type keyword **`global`** like in PHP).

If you specify a global variable, but not initialize it, it will return a **`nil`** pseudo-variable:

{% img center /images/global_var_assignment.png %}


======

**The Problem with Using Global variables:**

Global variables are incredibly easy to use (*I see sooo many games of Tic Tac Toe with global variables written by Ruby beginners*), but also quite easy to abuse as they cane be accessed from within anywhere in your code even though the code refers to two separate classes:

{% img center /images/global_variable_ill.png %}

Global variables violate the principle of [encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) by allowing one part of your code to modify another part of your code without an explicitly defined interface. Over-using them probably means that app was not thoroughly thought out.

======

**When to Use Global variables: Pre-defined Global Variables**

Even though global variables are generally considered to be un-Ruby-esque, Ruby does include a number of useful global variables (largely a Perl legacy) with a  **`$`** followed by a single character or a word that have a pre-defined meaning.

Below is just a selection of those, see a full list in [Ruby docs](http://ruby-doc.org/core-2.0.0/doc/globals_rdoc.html) or by running **`$global_variables`**:

{% img center /images/global_variables.png %}

Similarily, you can run  **`self.instance_variables`** on an class instance, or  **`Class.class_variables`** on a class.)

* **`$0`** -- contains the name of the script being executed. Is assignable.

{% img center /images/$0.png %}

* **`$0`** -- current line number of last line from input.

{% img center /images/$dot.png %}

* **`$:`** -- same as **`$LOAD_PATH`**, shows load path:

{% img center /images/load_path.png %}

* **`$$`** -- shows process ID (PID) of current script:

{% img center /images/pid.png %}

======

**Pre-defined Global Variables vs. Global Constants:**

Constants are an opposite of variables, but since Ruby has a number of global constants, I thought it would be good to briefly mention them as well.

The most commonly used global constants are **`ENV`** and **`ARGV`**.

* **`ENV`** gives access to environmental variables in a Ruby hash with variables as a hash key.

{% img center /images/ENV.png %}

* **`ARGV`** gives access to command-line argument values as strings in a Ruby array. It is also aliased as **`$*`**.

======

**Tracing Global Variables:**

Check out this RosettaCode screenshot [example](http://rosettacode.org/wiki/99_Bottles_of_Beer#Ruby) for the classic 99 Bottles of Beer coding exercise:

{% img center /images/rosetta_code_var_trace.png %}

The [docs](http://ruby-doc.org/core-2.2.1/Kernel.html#method-i-trace_var) say this re: **`trace_var`**:

> Controls tracing of assignments to global variables. The parameter symbol identifies the variable (as either a string name or a symbol identifier). cmd (which may be a string or a Proc object) or block is executed whenever the variable is assigned. The block or Proc object receives the variable's new value as a parameter. Also see Kernel::untrace_var.

This is the example that the Docs use:

{% img center /images/tracing_docs_ex.png %}

As you can see, one can pass a symbol that names a variable and a block of code or a string to the method. When the value of the variable changes, the block of code will evaluated or the string will be invoked (see more in [The Ruby Programming Language](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177/ref=sr_1_1?s=books&ie=UTF8&qid=1445989282&sr=1-1&keywords=9780596554651), 2008, p. 280)

Which means:

{% img center /images/global_var_tracing.png %}

And this is exactly how the 99 Bottles of Beer example works!

To stop tracing the variable, use **`untrace_var`** just like Ruby docs above specified.

