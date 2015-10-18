---
layout: post
title: "Rails Scaffold: Generating It, Deleting It, Evaluating Pros and Cons"
date: 2015-10-18 12:13:33 -0400
comments: true
categories: generators
---

Rails comes with a number of very convenient [generators](http://guides.rubyonrails.org/generators.html) that can take a lot of work out of creating models, controllers, views, tests, corresponding database migrations, etc.

Like many other developers, I use Rails scaffold generation as an efficient and convenient time-saver. 

From [Guides](http://guides.rubyonrails.org/command_line.html): 

>A scaffold in Rails is a full set of model, database migration for that model, controller to manipulate it, views to view and manipulate the data, and a test suite for each of the above.

Of course, you can generate all of those components individually as well, depending on your needs. But I think the scaffold generator in particular gets quite overused.

A regular scaffold Terminal command looks like this: `rails g scaffold Model_Name column_name:column_type:optional_index`

{% img center /images/scaffold_generate.png %}

`Model_Name` should be in singular, either under_scored or CamelCased.

Sometimes you hit the `return` button too soon, and deleting generated files by hand is just too much trouble.

There is a way to undo your entire scaffold: `rails d scaffold Generated_Scaffold_Name`:

{% img center /images/scaffold_destroy.png %}

(You can type out `generate` instead of `g` and `destroy` instead of `d`.)

Note that if you have already run `rake db:migrate` after generating your scaffold, the `destroy` command won't work. It will delete the files that the scaffold command has created, but it won't alter the schema and whatever alterations your migration has created will stay there. See my [previous post](http://annaershova.github.io/blog/2015/10/15/rake-database-tasks/) on database-related rake commands to learn how to fix that (you will probably want `rake db:migrate:down` or `rake db:rollback`).

And assuming you do version control, to see if the `destroy` command left any files, run `git status` or `git diff`.

Realistically speaking, to create a scaffold that later needs to be edited (say, a new migration created etc -- obviously a very common scenario) can cause more time-consuming bug-hunting than creating your MVC + other accoutrements from scratch. 

To generate a scaffold with tests (default option) stops a developer from proper test-driven development practices: writing a failing test first, and then making it pass.

You can of course pass in an option to prevent tests from being generated when creating a scaffold. Run `rails generate scaffold -h` to see a list of options in your terminal:

{% img center /images/scaffold_options_1.png %}
{% img center /images/scaffold_options_2.png %}

The options above are for Rails 4.2.0 and might be quite different for your version of Rails.

You can see that the command comes with a variety of options that allow for reasonable flexibility. For instance, to skip generating a migration, you can pass in `--skip-migration`. To skip creating tests, pass in `--no-test-framework`.

Ultimately, once you know exactly what you are building to the extent that you end up passing in a lot of options, you don't really need generators anymore and can create files manually that fit your needs. You wouldn't want to use it for production. But if you are just learning Rails and experimenting with it, generators are very handy.
