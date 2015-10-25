---
layout: post
title: "Making Custom Rake Tasks and Using Them With ERD"
date: 2015-10-13 08:52:15 -0400
comments: true
categories: rake, erd
---

I started making my own rake tasks recently to help with specific repetitive tasks that I need to do while working on projects.

Rake is a project of Jim Weinrich; check out his rationale for making rake [here](http://rake.rubyforge.org/files/doc/rational_rdoc.html).

My favorite part is his explanation of why it is called rake. No, it has nothing to do with garden tools. It was supposed to be a portmanteau of **'ruby'** and **'make'** (since Rake was inspired by Makefile). Hence, rake.

**`rake -T`** will give you a list of rake tasks available for a given project.

This is what it looks like for a standard octopress directory:

{% img center /images/take_t.png %}

So if I forget that my normal routine is **`rake generate`** followed by **`rake preview`**, I can see it listed above.

I was working with the [erd](https://github.com/voormedia/rails-erd) gem, which uses [Graphviz](http://www.graphviz.org/) to visualize complex database relationships in rails. If you want to understand what exactly is happening in your schema, it's the gem for you.

I haven't used it in a bit, so I googled it, and [this tutorial](https://ryanboland.com/blog/creating-a-database-diagram-with-rails-erd/) popped up.

It had a suggestion to make a simple rake task to run the erd command with specific attributes to get just the type of a diagram you want:

  ```ruby desc 'Generate Entity Relationship Diagram'
  task :generate_erd do
    system "erd --inheritance --filetype=dot --direct --attributes=foreign_keys,content"
    system "dot -Tpng erd.dot > erd.png"
    File.delete('erd.dot')
  end
  ```

The idea there is have a task that runs **`erd --inheritance --filetype=dot --direct --attributes=foreign_keys,content`**. The system then generates a **`.dot`** file, which is when converted into a **`.png`** file, with the rationale being that Graphviz has issues generating files that are not **`.dot`**. 

You can just put it in a rake file, or run **`rails g task erd generate_erd`**. It adds a **`erd.rake`** file to **`lib/tasks`** (or you can add one manually and just type your code instead of using a generator). 

To use that task, you type **`rake erd:generate_erd`** in your Terminal.

I ended up using these rake tasks to demonstrate the idea behind using namespace. They generate a **`png`** file as per an example above and a default **`pdf`** one:

{% img center /images/rake_commands.png %}

And running these tasks in Terminal:

{% img center /images/rake_terminal.png %}

And you are done! Two file types of database schema charts have been generated:

{% img center /images/erd_directory.png %}

NB: if all you wanted was to simplify running one long command (such as the aforementioned **`erd --inheritance --filetype=dot --direct --attributes=foreign_keys,content`**), you could just create a shell alias that you could then use across all your projects if they have erd installed. 





