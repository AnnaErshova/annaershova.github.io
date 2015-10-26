---
layout: post
title: "What about localhost:3000?"
date: 2015-10-26 12:10:56 -0400
comments: true
categories: localhost, server
---

Most people new to rails go through some sort of 'make-an-app-in-under-15-minutes' tutorial, which always includes instructions to run **`rails s`** or  **`rails server`** to get a preview of your app.

Typing it into a console usually produces something like this:

{% img center /images/railss.png %}

That means that a Rails server is now listening on port 3000.

And when you point your browser to **`localhost:3000`** (or alternatively **`http://127.0.0.1:3000/`**, where **`http://127.0.0.1`** is your computer's loopback address), you see the standard Welcome Aboard message:

{% img center /images/localhost_screenshot.png %}

Of course that is the case where the app is either blank (so that going to leads to a blank website or no root page has been set up) so that when you click on [http://localhost:3000/rails/info](http://localhost:3000/rails/info) with server running, you see this:

{% img center /images/rails_info_routes.png %}

(note that it only works for development environment; once your app is deployed, say, **`my-app.herokuapps.com/rails/info`** won't work unless you have built that route and populated it.)

In fact, **`localhost:3000`** is so common that someone registered a [website](http://www.localhost3000.org/) that takes you to a website that reminds you you forgot to start your server, if that is indeed the case.

Note that when using Chrome, you can just type in **`localhost:3000`**, but for Internet Explorer, you would need to point your browser to **`http://localhost:3000`**, otherwise, you will see an error message.

======

Once your app has a model or two and corresponding migrations have been run, you will be able to point your browser to, say **`localhost:3000/users`** if a User model is present.

======

**What if I want to use another port?**

To switch port to, say, 80, run this:

**`rails server -p 80`**

You might need to prepend it with **`bundle exec`**.

See documentation on it [here](https://github.com/rails/rails/blob/4-2-stable/railties/lib/rails/commands/server.rb) as I could not find any actual description in Terminal:

{% img center /images/rails_server_docs.png %}

**`rails s`** will run as development, not production, by default. To change port for a different environment, run something like:

**`rails server -e production -p 4000`**

======




