---
layout: post
title: "Mac Uptime and Reboot Stats"
date: 2015-10-12 11:46:01 -0400
comments: true
categories: terminal
---

While we are on a subject of controlling your Mac from your Terminal, here is something else that is useful:

Mac uptime is how long it has been since the system has been re-booted or re-started. Type in **`uptime`** in your Terminal, and you will see the stats in minutes, hours, or days, depending on how long it has been for your Mac:

{% img center /images/uptime.png %}

(I just re-booted when installing a new OS X hence such a short uptime for me. Uptime can extend into months for some users as Macs tend to be very stable unlike Windows machines.)

You will also see number of users using your machine during said uptime as well as load averages in 1, 5, and 15 minute intervals from left to right -- mine actually indicate I may want a more powerful system.

Run **`last reboot`**  to see rebooting history:

{% img center /images/lastreboot.png %}

Another neat trick is to run in **`last`** to see last sessions of users, hosts and ttys in a reverse chronological order:

{% img center /images/last.png %}

There are handy gadgets for uptime and reboot stats, but I doubt that most regular users would really need them on a regular basis. Checking in with your Terminal now and then should be sufficient.