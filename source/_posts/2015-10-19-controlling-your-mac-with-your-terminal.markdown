---
layout: post
title: "Mastering Your Terminal -- Part I"
date: 2015-10-19 16:15:58 -0400
comments: true
categories: terminal
---

Developers tend to spend a lot of time in their Terminals, and while most know all the basic commands to run, there are some that are less commonly used, but quite nifty to know.

In an [earlier post](http://annaershova.github.io/blog/2015/10/12/updating-os-x-from-your-command-line/), I mentioned that one can use command line to run a software update command: `softwareupdate -l` to see what updates are available:

{% img center /images/softwareupdate_list.png %}

Terminal, or more accurately, Terminal.app, is a terminal emulator program that provides a connection to your shell (most likely **`bash`**; run **`echo $0`** to see what yours is running). 

Technically speaking, running commands in Terminal is really running commands in a command-line interface that runs in a shell that runs in Terminal.

Now that we got that out of the way -- 

**Some basic tricks**:

* **`Up`** or **`down`** key to navigate between commands. I use **`up`** all the time when navigating to a previously used command that is too long to type again.

* **`!!`** to repeat last command (this will be specific to your Terminal window or tab in which you run it)

{% img center /images/bang_bang.png %}

Ok, it is actually easier to press the **`up`** arrow once, but hey, saying *bang bang* out loud is a lot more fun. 

* Drop file name from Finder into terminal to get its path -- it can be then copy-pasted into a **`cd`** command etc.

**More ways to navigate Terminal using familiar shortcuts**:

* **`Ctrl + T`** to open a new tab within the same Terminal session.

* **`Ctrl + F`** to search your Terminal's tab or session (actual text output thereof).

* **`Command + +`** or **`Command + -`** to zoom in or out.

*  **`Command + G`** to go to a next search match, **`Command + Shift + G`** to go to a previous match.

* **`Control + C`** or **`Command + .`** to cancel a command. Rails developers use that a lot to stop Rails server from running, for instance.

* Use **`TAB`** to autocomplete a directory name. Use **`TAB`** **`TAB`** to show a list of options when there are multiple matches.

**Who am I, where am I, and what time is it anyway?**

* **`pwd`** to see user's current directory:

{% img center /images/pwd_use.png %}

* **`whoami`** to see username of the owner of the current login/connection session in the shell (or in manual's words, "display effective user id")

{% img center /images/whoami.png %}

* While **`whoami`** is a very commonly listed command in all of the top-20-Terminal-commands-you-must-learn-now list, its cousins **`WhoAmI`** and **`who am i`** are less known:

{% img center /images/whoami_variations.png %}

(There is no manual entry on **`WhoAmI`**, and that seems like a pretty rare command in general.)

* Another cousin **`who`** displays a more expanded version of **`who am i`**, effectivly showing all users that are currently logged in into a terminal session:

{% img center /images/who.png %}

* And yet another cousin **`w`** "displays who is logged in and what they are doing:

{% img center /images/w_command.png %}

* **`date`** to see current date and time:

{% img center /images/date_command.png %}

**How do I get around?**

* **`cd directory_name`** or **`cd path/to/directory`** to move to a different directory

* **`TAB`** can be used with **`cd`** to autocomplete a directory name, but using an asterix (*) as a wildcard also works:

{% img center /images/cd_wild_card.png %}

* **`?characters`** to search for a specific name:

{% img center /images/cd_wild_card.png %}

* **`cd ..`** to move up one directory, **`cd ../..`**  to move up two directories, and so forth.

* **`cd ~`** or just **`cd`** to go to your home directory.

* **`cd /`** to go to the level of your file hierarchy (this is not the same as home):

{% img center /images/root_vs_top.png %}

* **`cd -`** to go to the last visited directory:

{% img center /images/cd_minus.png %}

* Note on case sensitivity: generally, names of files and directories (so that **`cd octopress`** is the same as **`cd Octopress`**) are not case sensitive unless you have specially set up your system to be that way.

**So what am I seeing in here?** 

* **`ls`** to see a list of files in your directory (or **`ls directory/path`** for another directory)

{% img center /images/octopress_ls.png %}

* **`ls -l`** to see a *l*ong list of files, including creation dates and access permissions, number of links in the item, etc:

{% img center /images/du_sh.png %}

* **`ls -lh`** or **`ls -l -h`** (flags can be combined) to see a *h*uman readable output as long list. In this case, the only thing that changes is size in bytes is converted into units that make more sense such as kilobytes. Note that **`-h`** flag can be use with some other commands as well.

{% img center /images/ls_lh.png %}

(Try running **`ls`** first, then **`!! -l`**, then **`!! -h`** to stack these commands. Or just press an **`up`** key and add those flags before hitting enter).

* **`ls /`** (or any other **`ls`** command with a **`flag`** and **`/`**) to see contents of home directory. Note that normally, you have to be in the directory which contents you are trying to view.

* **`du -sh directory_name`** to see size of a directory:

{% img center /images/date_command.png %}




