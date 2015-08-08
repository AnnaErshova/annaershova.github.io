---
layout: post
title: "On a Scale of Dalai Lama to Kanye West, How Narcissistic Are You? A Rails App That Lets You Find Out Just That."
date: 2015-07-26 09:32:26 -0400
comments: true
categories: Flatiron School
---

For a small side project to be shared with our Flatiron School classmates and some [Flatiron School Presents Meetup](http://www.meetup.com/Flatiron-School-Presents/) guests, my partner Mitch and I decided to build an app that measures people's narcissism levels via their Twitter feed. A linguistic analysis-baased social insights algorithm, if you will.

{% img center /images/kanye-meme.png %}

(meme taken from [here](http://knowyourmeme.com/photos/688363-kanye-west) -- spoiler alert for celebrities' narcissism levels)

Much has been said and done and invested into when it comes to social media sentiment analysis in finance, with many financial institutions investing heavily in it. A cursory Google search offers up names of many start-ups involved in mining, mapping, analyzing, and plain having fun with Twitter. We figured that as tech professionals, working with social media and building a fun prototype for understanding the tools and the medium is a valuable experience.

Our original idea was parsing through people's Instagram feed to see how many posted photos were selfies for a better narcissism indicator, but considering advanced facial recognizition technology needed and the fact it was meant to be a small side project executed while carrying on a full school work load, we have settled on the twitter-based project.

The [Twitter gem](https://github.com/sferik/twitter) made working with Twitter a breeze, although there were limitations for how many posts could be parsed through at once and of course the max number of timeout requests every minute.

We designed everything through the use of good ol' Rails New NarcissismProject. We had one user model that we worked with. 

The front page invites a user to check how narcissistic the are by entering a twitter handle (which will work whether or not prefixed with an @ to make user's life easier; we have also allowed for the first or last typed character to be blank space in case a user is very space-key-trigger-happy; other than that, the handle has to follow Twitter rules as ensured by a RegEx check):

{% img center /images/narcissism-app-front-page.png %}

Once a user enters a twitter handle, it parses their feed for key narcissism-related words that we have pre-determined in the app; it then checks it against a scale of celebrities. It then returns user's score and their celebrity match (mine is Flatiron School's very own [Avi Flombaum](https://twitter.com/aviflombaum))

We don't share the celbrity scale on the app, as it is more fun for the user to discover it him/herself. To built it, we have parsed through the top 100 most-followed twitter accounts (most of which are individual celebrities) and some more and scored them. We then picked some representatives for each scale gradation, throwing in a few Flatiron School-related Easter Eggs, just for fun. If this was a commercial product, we would have to update the celebrity scale just in case some of them go into narcissism rehab or new self-loving celebrities merger.

Most of our findings were unsurprising: Dalai Lama and the Pope were at the very bottom (with Dalai Lama being slightly less narcissistic and thus representing no. 1 on our scale); Kanye West was 9 out of 10 (beat only by the likes of Lena Dunham); Mr. West was closely followed by Kim Kardashian in the 8th place. To me, this means that are simplistic prototype algorithm actually works!

I stopped to pondered if it is unethical to make fun of people's narcissism levels, but considering the celeberities that came up on top and their interest in self-promotion, I figured out their high tankings it would be quite a compliment to them (I am really, really tempted to tweet Mr. West and ask him how he feels about being outdone by Ms Dunham).

What turned out to be incredibly fun was soliciting our friends' and classmates' twitter handles and checking their narcissism levels. A few were truly off-the-charts! (We even had to design more model logic for those cases) The top 10 narcissistic twitter handles are then saved separately and published on the Top 10 page -- with many people I know outdoing our celebrities of choice. Uh oh.

A short demo video can be found [here](http://youtu.be/T_tTweOvDqs) -- YouTube link.

And here is a link to the Github [repo](https://github.com/mitchellhart/twitter_analyzer).

I will update this post once the app actually goes live as is our goal.