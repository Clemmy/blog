---
title: "A Breakdown of my Weekend at UofTHacks"
tags: [meteor, hackathon]
layout: post
date: 2015-02-05
---

Hello everyone! This past weekend, I attended [UofTHacks](https://www.hackerleague.org/hackathons/uofthacks), which was a hackathon hosted by the University of Toronto. I had very high expectations for the quality of this hackathon, but it seemed to fall a little short of what I imagined. Perhaps my expectations were set so high because the University of Toronto was one of the biggest schools in Canada, or perhaps it my mood was simply a bit grumpy that day. Either way, let's begin this post with a critique of UofTHacks and hopefully, I won't be too harsh:

- I received my UofTHacks shirt in size L, one size too big for me, even though there was a form online that all attendees had to fill out, including their shirt size
- There weren't that many employer booths - No free swag. :(
- There weren't many late night events - most of my time was spent in a small room coding for hours and hours on end
- Their brunch could use some work: [A wonderful photo of the food]({{ site.baseurl }}/assets/in_post_images/uoft_brunch.jpg)
- The atmosphere seemed a little dead - while I was at Hack the North, I was able to constantly walk around and meet new people. In fact, I even had someone from another team help me out with a problem that I had been stuck on, spending hours of his time to help me out. It was a great experience and I met a lot of friendly people. However, at UofTHacks, there was very little interaction with others, so it led to a very awkward environment

However, most of these downfalls can be attributed to a lack of experience in hackathon organization, and also a low budget. I noticed that the number of sponsors at UofTHacks were few compared to Waterloo's Hack The North that I attended last year, so that may have been the reason for its scarcity of events. Despite these downfalls, I still saw the effort that was put into this event. Although few, the volunteer workers were very nice and put a lot of spirit into cheering everyone on and doing their thing. In addition, there were some memorable events such as Red Bull's paper plane challenge to see who can build the farthest gliding paper airplane. I will still have high expectations for UofTHacks in the future. Not many people it right their first time, and they will have plenty of time to learn from this experience, and be _amazing_ next year. I will definitely be applying again.

Alright, onto the butter of this post!

## Who?

I teamed up with two friends of mine for this hackathon. One was my buddy [@ramanpreetnara](https://github.com/ramanpreetnara), who is a JavaScript master that has taught me the ways of JavaScript, as well as a friend of mine who specialized in frontend, [@jerryzxliu](https://github.com/jerryzxliu). After we gathered, we decided to make an organization for all future hackathon projects, and so [parasitic](https://github.com/parasitic) was born. Check it out!

## What?

Unfortunately, none of us went into the hackathon very prepared, so we had no ideas on what to do upon entry. After a few hours of brainstorming, we decided to go along with something that I was planning to make eventually: [hearthnet](https://github.com/parasitic/hearthnet). Basically, it is a platform for finding and challenging other players in a game called Hearthstone, which I mentioned in an earlier blog post, since the game has no innate feature to allow users to find each other based on deck preferences and other fields.

## How?

For this project, we wanted to learn a new framework. After a bit of discussion, we decided to go with [Meteor](https://www.meteor.com/), which is a full stack JavaScript framework, since one of our close buddies used it to build [Phanime](http://phanime.com/), which we regard as a pretty neat website. We all spent a few hours reading up on some Meteor basics before our hacking began!

## The Workflow

The workflow that we used at this hackathon was quite different from the Git flow workflow that we use at my workplace, which aims to keep the Git tree clean. Right away, a spike branch was created, and ramanpreetnara and I pair programmed to write a big chunk of code which supported authentication and allowed the web app to route properly. Interestingly, it was hard to decouple the work process at first because Meteor is interesting in that its programming paradigm encourages interaction to a published database in the client-side, and has a big feature known as reactivity. Once we got a solid base to work on, we all branched off to different features and worked individually, using a merge-heavy approach to combine our changes.

## Some downfalls

One downfall that we had was that while jerryzxliu is experienced in Zurb Foundation, a frontend framework, ramanpreetnara and I had nil. We thought it would be okay as long as jerryzxliu handled all the frontend work, but the framework itself didn't play too nice with Meteor, and we were blocked for a while in trying to bootstrap everything. In addition, the #nosleep hackathon culture took its toll on jerryzxliu and he had to leave prematurely. Also, it was our first time trying to implement user authentication, and since we were rushed on time, we ended up doing it incorrectly (using client-side routing instead of a server sided solution). This will have to be rewritten in the future for hearthnet to be more secure.

## Some cool things I learned

- Meteor reactivity: All layers, from database to template, update themselves automatically when necessary. This is done with some Meteor magic where a the client has a local copy of the 'published' content of the Mongo database on the server, and most operations are actually performed on both the client and server side, then their results are compared, which increases the speed of the client site, as well as an additional security check

- Authentication in Meteor literally takes a couple of lines (for a very basic bcrypt implementation without styling):

{% highlight javascript %}
meteor add accounts-ui accounts-password
{{> loginButtons}}
Accounts.ui.config({
  passwordSignupFields: "USERNAME_ONLY"
});
{% endhighlight %}

That is all I have for tonight folks! But there are a lot of things I want to blog about soon, including some interesting problems I've faced at work, how to use Git properly, as well as other cool things. Be sure to keep updated!
<!--end-->
