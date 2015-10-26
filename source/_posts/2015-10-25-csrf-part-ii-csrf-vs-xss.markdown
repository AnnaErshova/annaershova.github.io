---
layout: post
title: "CSRF Part II -- CSRF vs. XSS"
date: 2015-10-25 18:03:57 -0400
comments: true
categories: CSRF, security, XSS
---

I touched upon CSRF (cross-site request forgery) in my [previous blog post](http://annaershova.github.io/blog/2015/10/25/whats-csrf-and-what-exactly-are-we-are-protecting-from-forgery-in-controllers/), but as I was mentionining that it is distinct from XSS since the two get mixed up sometimes (must be the multi-fricative-consonant abbreviation), I realized that I should discuss it in greater detail.

======

**Web Attack Types Vulnerabilities: Gotta Catch 'Em All**

Both XSS abd CSRF are types of web attacks (there are more than these two, but I have seen people get them confused, and they do have interesting parallels). XSS is *cross-site scripting*. CSRF, as previously mentioned, is *cross-side request forgery*.

**The fundamental conceptual difference between CSRF and XSS is that CSRF exploits a website's trust (authentication) of a user, whereas XSS exploits a user's trust for a website.**

======

**XSS: The Mechanics**

XSS involves injecting malicious scripts (in the case of Rails, it would usually be JavaScript, potentially combined with HTML, often with a **`<script>`** tag) into a webpage. That script can be then executed when other users access the website. 

For instance, a hacker introduces some JavaScript to the comments section of a webpage, and when other users try to access it, the script is executed and, say, the user is re-directed to a porn website they otherwise from their original destination S.H.I.E.L.D. subreddit.

XSS attacks are incredibly common and easy to execute if a website does not have appropriate security features.

======

**XSS and Ruby on Rails: Opting Out of HTML Escape**

As with CSRF, Rails comes with a reasonably strong protection against XSS attacks. That certainly makes life easier for most beginners who want to have a reasonably secure website without spending too much time researching security and focusing on building other skills first.

The idea behind Rails XSS protection is automatically sanitizing user input so that nothing gets executed as a script if it's not meant to be. Back in the day, that had to be done manually, which, was extremely time-consuming and error-prone. So Rails 3 incorporated a simple idea: opting out of html escaping instead of opting in, if need be.

It accomplished that by integrating **`RailsXss`** [plugin](https://github.com/rails/rails_xss), and the feature [became part of Edge Rails](https://github.com/rails/rails/commit/9415935902f120a9bac0bfce7129725a0db38ed3) as early as [October 2009](http://weblog.rubyonrails.org/2009/10/12/what-s-new-in-edge-rails/) (see more on Edge Rails in my post [here](http://annaershova.github.io/blog/2015/10/11/running-edge-rails-living-dangerously/) ). 

Rails 3+ officially supports this feature, and it backports to earlier versions of Rails as well.

I noticed from reading [source code](https://github.com/rails/rails/blob/4-2-stable/activesupport/lib/active_support/core_ext/string/output_safety.rb) that Rails now assumes that no string input is **`html_safe?`** by default, while integers are:

{% img center /images/object_vs_numeric.png %}

This is what it looks like in Rails console:

{% img center /images/html_safe_int.png %}

Html escape it can be still done manually with an [**`html_escape`**](http://api.rubyonrails.org/classes/ERB/Util.html#method-c-html_escape) in front of whatever you are rendering within the erb tags. 

**`html_escape`** can be also aliased as **`h`**, and it is fine to use it even if something is getting html escaped by default as Rails will recognize it as such and will only escape it once.

See example from [source code](https://github.com/rails/rails/blob/4-2-stable/activesupport/lib/active_support/core_ext/string/output_safety.rb):

{% img center /images/html_escape.png %}

The potentially 'dangerous' charactaters are converted into their human-readable equivalents as the same source code indicates:

**`HTML_ESCAPE = { '&' => '&amp;',  '>' => '&gt;',   '<' => '&lt;', '"' => '&quot;', "'" => '&#39;' }`**

Similarily, [**`html_escape_once`**](https://github.com/rails/rails/blob/4-2-stable/activesupport/lib/active_support/core_ext/string/output_safety.rb) escapes HTML code without affecting existing escaped code:

{% img center /images/escape_once.png %}

If you do not want user input to be sanitized, then using **`raw`** in the erb template is the way to go, e.g.:

{% img center /images/rawxss.png %}

======

**If That Were Not Enough**

[Wikipedia article](https://en.wikipedia.org/wiki/Cross-site_scripting) is a good starting point.

This [Railscast episode](http://railscasts.com/episodes/204-xss-protection-in-rails-3?autoplay=true) is worth spending 8 minutes on, even though it is a bit older.

And as usual, more on XSS on the [Rails Guides](http://guides.rubyonrails.org/security.html#cross-site-scripting-xss) website.