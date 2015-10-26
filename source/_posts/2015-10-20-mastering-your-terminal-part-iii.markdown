---
layout: post
title: "Mastering Your Terminal -- Part III"
date: 2015-10-20 23:24:26 -0400
comments: true
categories: terminal
---

**Shutting Down Your Mac From Your Terminal:**

**`sudo shutdown -r now`**

**`shutdown`** is the command you need.

Pass in the following options:

* **`-h`** -- halt the session, re-starts the system 
* **`-s`** -- sleep
* **`-r`** -- re-boot the system
* **`-k`** -- kick everyone off but the super-user

And as for time options:

* **`now`** -- execute command immediately
* **`+integer`** -- execute command in x minutes (e.g., **`+10`** is in 10 minutes)
* **`yymmddhhmm`** -- execute command on a given time and date

If you schedule a **`shutdown`** command, but decide to hold off of it, **`sudo shutdown -c`** will cancel it.

In my understanding, **`sudo shutdown -r now`** is a functional equivalent of **`sudo reboot`**

======

**Changing What Your Power Button Does:**

In the OS X prior to the 10.9 Maverick, a power button used to bring up a **`Restart`**, **`Sleep`**, **`Cancel`**, and **`Shut Down`** options.

In later OS X versions, pressing it just puts your machine to sleep. If you want to have it bring up an earlier options menu, run this:

**`defaults write com.apple.loginwindow PowerButtonSleepsSystem -bool FALSE`**

Pressing the power button will then bring up this dialog:

{% img center /images/powerbuttondialog.png %}

If you want to switch back to the sleep-only option, run the same command with **`TRUE`** instead of **`FALSE`**.

======

**Having Your System Restart Automatically If It Freezes:**

While Macs tend to have relatively good uptimes (see [here](http://annaershova.github.io/blog/2015/10/12/mac-uptime-and-reboot-stats/) for more info what that is and how to find it out), OS X can still freeze up. Most users press the power button for a couple of seconds to have it turn off, and then press it again to turn it back on. That generally works well, but you can also type this in your Terminal to have its equivalent happen automatically:

**`sudo systemsetup -setrestartfreeze on`**

(It's also useful if you are not there physically to press the restart button, for instance, if your Mac acts as a server.)

To disable this option, run the same command with **`OFF`** instead of **`ON`**.