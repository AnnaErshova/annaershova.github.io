---
layout: post
title: "What's CSRF and What Exactly Are We Are Protecting From Forgery?"
date: 2015-10-25 14:53:44 -0400
comments: true
categories: CSRF, controllers, security
---

Running any **`Rails new`** command will produce a **`ApplicationDirectory/app/controllers/application_controller.rb`** file that looks like this initially:

{% img center /images/application_controller_csrf.png %}

Since Rails is so beginner-friendly, many new developers are too preoccupied with making an app that works (*why do my routes look like that?!*) than looking into each and every line of generated code. I find that the CSRF-related line of code in a standard **`ApplicationController`** is particularily often overlooked. I wanted to discuss it here as it is connected a serious security issue often encountered on the web.

The Ruby on Rails API has a comprehensive [guide](http://api.rubyonrails.org/classes/ActionController/RequestForgeryProtection/ClassMethods.html) explaining what **`protect_from_forgery`** does. It still assumes a basic understanding of CSRF. 

CSRF, just like XSS, which will be discussed in the next post, is not a Rails-specific problem, and it really affects all computer systems and all languages, although this post will discuss in the context of Rails.

======

**How CSRF Works**

CSRF (sometimes spelled as XSRF) stands for *cross-side request forgery*. It is, according to [Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery), sometimes pronounced as *see-surf* (which I absolutely did not know prior to reading the Wiki article). However it is pronounced, it involves an attacker submitting malicious commands to an app that appear to come from a user that the app has authorized and that the browser trusts. The hacker can therefore gain control of an account.

CSRF is sometimes refered to as 'session riding,' a pretty accurate description as you'll see.

Note that this is different from XSS (cross-site scripting).

Most Rails apps use cookie-based sessions. If an attacker can find a link s/he can reproduce (*forge*) that involves executing something on a target page while a user is logged in, they can then embed such a link -- with a malicious action -- on a page where a user can click it, thus giving an attacker control of the account.

It is not uncommon for websites to be vulnerable to CSRF attacks. At various times, some major websites such as YouTube, The New York Times and INGDirect [famously](http://www.darkreading.com/risk/csrf-flaws-found-on-major-websites/d/d-id/1129743) all had that issue. 

In INGDirect case, hackers could gain control of users' accounts and transfer money out to an account that was open in user's name but was not actually associated with them. In YouTube's case, hackers could friend other users on behalf of a hacked user, add videos to the user's favorites, and send messages on a user's behalf.

A web developer generally needs to explicitly protect their app from CSRF attacks, and thankfully, Rails does it for us with default code. (Other languages often have plugins etc to help handle this issue, but Rails, as usual, makes things much easier.)

======

**What Is Protect_From_Forgery?**

According to to the [Rails source](https://github.com/rails/rails/blob/0450642c27af3af35b449208b21695fd55c30f90/actionpack/lib/action_controller/metal/request_forgery_protection.rb): 

> Controller actions are protected from Cross-Site Request Forgery (CSRF) attacks by including a token in the rendered HTML for your application. This token is stored as a random string in the session, to which an attacker does not have access. When a request reaches your application, Rails verifies the received token with the token in the session. All requests are checked except GET requests as these should be idempotent. Keep in mind that all session-oriented requests should be CSRF protected, including JavaScript and HTML requests.

That means that your app will protected against CSRF attacks with one line in your Application Controller: **`protect_from_forgery with: :exception`**. 

======

**How Is Protection Executed?**

General principle of CSRF protection is introducing user-specific secret data into the request that would not be accessible by a hacker. That is exactly how Rails does it. It protects your session via a **`:null_session method`**: an empty session is generated during a request. 

It requires that a special CSRF token is present before any **`POST`**, **`PUT`** or **`DELETE`** request is accepted. That token will be included as a hidden field when using Rails forms builders. (Most browsers only support **`GET`** or **`PUT`** instead of all the proper RESTful verbs, but we know that Rails uses a hidden field **`_method`** to fix it.)

**`GET`** requests are not protected since they don't have potential to leak sensitive data. That is why it is important to use **`GET`** requests appropriately in cases when a database is read or queried etc, but a user's state in the app is not modified.

The required security token in question is known as **`authenticity_token`**. That token is known to its app, but not to others. To achieve that, its name and value must be added to every view that renders forms by adding **`csrf_meta_tags`** within html **`head`** tags. That is also a default option generated when using a **`Rails new`** command and places into a **`ApplicationDirectory/app/views/layouts/application.html.erb`** file, which is normally the only view file generated for a model-less app: 

{% img center /images/applicationhtmlerb.png %}

It's interesting to see the [source code](https://github.com/rails/rails/blob/4-2-stable/railties/lib/rails/generators/rails/app/templates/app/views/layouts/application.html.erb.tt) for this in the Rails repo:

{% img center /images/applicationhtmlerblayout.png %}

Is a CSRF token does not match, Rails will raise an **`InvalidAuthenticityToken`**.

======

**What if I am running tests?**

To disactivate this feature for the test environment:

**`protect_from_forgery unless Rails.env.test?`**

======

**What If I am Building an API?**

Since XML or JSON formats are also affected by this code, default forgery protection should be turned off if you are building an API as the API is designed to be stateless: **`protect_from_forgery unless: -> { request.format.json? }`**

There is more information on the [Rails Security Guides](http://guides.rubyonrails.org/security.html).

