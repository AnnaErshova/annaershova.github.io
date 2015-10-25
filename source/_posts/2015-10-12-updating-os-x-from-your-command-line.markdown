---
layout: post
title: "Updating OS X From Your Command Line"
date: 2015-10-12 11:16:32 -0400
comments: true
categories: Terminal
---

I am really used to seeing a pop up that says something along the lines of **`a new version of OS X / iOS is available, do you want to update now?`**

Upon some research on potential issues of an update in question (I learned the hard way after having my iPhone bricked post-update when living in China), I generally go back and click **`update`**. But there is actually an easy way to do it from your Terminal. All you need is a **`softwareupdate`** command.

Type in **`man softwareupdate`** to see this command's manual:

{% img center /images/softwareupdatemanual.png %}

Run **`softwareupdate -l`** to see available updates. You will see something like this:

{% img center /images/softwareupdate_l.png %}

While you are at it, you can turn on automatic update checker from your Terminal: **`sudo softwareupdate --schedule on`** (**`off`** to disable it).

{% img center /images/softwareupdateautomaticcheck.png %}

Then run this to install the specific update you want: **`sudo softwareupdate --install UPDATE_NAME`**

{% img center /images/supdinstall.png %}

(Use the **`-d`** flag to just download the update, but not install it.)

And of course to re-boot your computer, you can simply run this command instead of going through the Mac menu: **`sudo shutdown -r now`**

{% img center /images/shutdown.png %}

Voila!


