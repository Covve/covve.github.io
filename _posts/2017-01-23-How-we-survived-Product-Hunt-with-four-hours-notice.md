---
layout: post
title:  How we survived Product Hunt with four hours' notice
categories: Team
cover: /images/blog/2017-01-23-How-we-survived-Product-Hunt-with-four-hours-notice/1.png
author: ap
---
For those of you not aware of it, Product Hunt is a website that features the world’s coolest new software products every day. It has tons of followers and being featured on PH can mean massive exposure in a period of just 24 hours.

It’s also a tech team’s worst nightmare.
<!--more-->

#The news-bomb

But lets start at the beginning. It’s a peaceful Friday morning at Covve HQ, the team busy between our Friday brown bag sessions and developing new cool features, when suddenly an email drops from the ether:

> Guys, in 4 hours you’ll be featured on PH

The business side of the brain opened a small mental champagne. The tech side had a small mental heart attack.

Why? Because being featured on PH can mean anything from tens of thousands of hits an hour to tens of signups per second! In short – a burst in traffic that is exceedingly out of the ordinary and most likely way beyond a young startup’s tech limitations.

So what do you do when news like this drops and the clock is ticking – you gather the team and whip out the whiteboard of course. (and grab coffee and let wife/boyfriend/parents know you’ll disappear in a black hole for 24 hours).

With warm cups of coffee and Covve’s architecture diagram on the wall we started agreeing a scaling approach for each part of the system.

#Scale, one piece at a time

##Databases

We get SQL as a service so this one was relatively easy – throw money at it and scale up to the best the platform has to offer. An important point of detail though: make sure scaling operations don’t affect your live users.

Orient DB is next on the menu. This one is deployed as IaaS and in all likelihood would have been sufficient as-is. However, to be extra safe we decided to scale up. This was added to the list of changes for the “PH build” we’d prepare over the course of the next hours.

Elastic Search, again on IaaS, didn’t need bigger machines – it needed more of them. Auto-scaling was already setup so we just needed to provision a few extra servers to raise the upper limit of the scaling operation to five servers.

##Background workers

All of the heavy lifting at Covve is done by a series of very small and very scalable workers. For example the sync service that synchronises individual contacts with Google, Exchange or iPhone or the dedupe service that identifies duplicate contacts.

These workers were explicitly architected to have the smallest business as usual footprint (each virtual server is tiny and consumes very small units of work) and be able to massively scale-out on demand. This way cost is kept low without limiting the total throughput achievable.

As such it was simply a matter of changing our scaling settings from a few servers to a few hundred of each type.

##API

The Covve API is hosted on managed PaaS (complete with public load balancing etc.). This one just needed scaling out (a 5 second job).

##Website

The public website is hosted on IaaS and serves an optimized WordPress site so a bit of scale up did the trick.

##External services

Following the principle of not reinventing the wheel we use external services wherever we can. Services such as MapBox for serving maps, Mandrill for emails and LogEntries for log management to name a few. For each of these we’d need to review our usage quotas and, where needed, beef up the subscription for the month.

Overall we were looking at scaling up and out our architecture by a factor of around ten – with, now, three hours to go.

#Tick tock.

By t-1:30 the scaled-up “PH build” was ready to deploy

By t-1:10 the build was deployed and final configuration had begun

By t-0:40 all scale-out settings had been configured and external services were updated as required. The team was spot testing all aspects to make sure nothing had slipped between the cracks

By t-0:30 … it happened. Half an hour earlier than expected, Covve was featured on Product Hunt

The next ten hours were a mixture of elation and anticipation. With each person responsible for monitoring a specific part of the system (from Google analytics to queue sizes to response times to server loads to deep down in the trenches logs), all screens were covered in monitoring and stats. And, as promised, the traffic came and it came in spades. All figures across all consoles were orders of magnitude higher than what we’d ever seen.

Our website visits were up 6000%, signups were up 4000% and the total number of contacts managed by Covve went up by several hundred thousand – in the space of 10 hours. That’s hundreds of thousands of contacts that were synchronized, analysed, enhanced with metadata (locations, industries, companies, seniorities, avatars etc.), deduplicated, indexed and synced back.

And despite all this (and to my suspicious disbelief) everything had worked like clockwork. Zero downtime, zero issues, zero degradation. And, at a very reasonable cost – just a 30% spike in our monthly infra outgoings. We even had spare time for office pizza and celebratory drinks.

![Celebration](/images/blog/2017-01-23-How-we-survived-Product-Hunt-with-four-hours-notice/2.jpg)

Thinking back I shouldn’t have been sceptical – every aspect of Covve’s architecture from the very first line of code has been built to scale – and scale big time. The whole exercise was a great proof of the value of doing things properly and aiming high from the outset. It was also great testament to the value of a tightly knit team who know their stuff.

<em>Note: This article was first posted on [http://covve.com/blog][eventualconsistency] in 2015 - it has been reposted here for the benefit of inside.covve.com's audience</em>

[covvesblog]: http://covve.com/blog