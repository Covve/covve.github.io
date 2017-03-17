---
layout: post
title:  Pet project day - Feb 17 - Anti-patterns, PWA and push notifications
categories: Engineering
cover: /images/blog/2017-03-17-Pet-projects-day-2/petproject.png
author: ap
---
The last Friday of each month is Pet Project day over here at Covve. Giving ourselves the time to experiment with new and exciting technologies, try out new approaches or just scratch that technological itch.

February’s pet projects ranged from an experimentation with progressive web apps to putting our code's deisgn to test against Martin Fowler's personal pet hate, the anemic model anti-pattern
<!--more-->

### Andy and Zafeiris: The anemic domain model anti-pattern (a cost/benefit analysis)

![AnemicModel](/images/blog/2017-03-17-Pet-projects-day-2/anemicmodel.png)

Discussions into correct design, use of patterns and maintainable and future proof code is quite common around the water cooler. 

So, with a statement as powerful as the above, from an authority as credible as [martin][Martin Fowler], Zafeiris and Andy just couldn't resist joining forces and putting our code to the test.

[anemic][Anemic models], in Martin's words, are objects which, when you look at their behavior, you realize that there is hardly any behavior on them, making them little more than bags of getters and setters. They're considered an anti-pattern because they incur all of the costs of a domain model, without yielding any of the benefits.

This pet project searched for occurences of this anti-pattern in the codebase of our cross-platform app and evaluated both why they came about and the implications (both cost and benefit) of addressing them.

More importantly it established an agreed approach for dealing with such occurences going forwards.

### Iasonas: Experimenting with progressive web apps

![pwa](/images/blog/2017-03-17-Pet-projects-day-2/pwa.png)

Iasonas is the newest member of the cross-platform (XP) team, focused these days on the [ionic2][Ionic 2] and [Angular2][Angular 2] aspects of Covve's next generation app. The XP app is currently in production on Android and is planned to replace the existing native iOS app in due course.

In many ways the Covve cross platform app already meets the definition of a [pwa][Progressive Web App] (PWA), namely:

"Progressive Web Apps are user experiences that have the reach of the web, and are:
- Reliable - Load instantly and never show the downasaur, even in uncertain network conditions.
- Fast - Respond quickly to user interactions with silky smooth animations and no janky scrolling.
- Engaging - Feel like a natural app on the device, with an immersive user experience."

And yet the cross platform app is, by definition, a mobile app and is not currently envisaged to replace Covve's Single Page Web Application (SPA). The main reason being that although the business domain is indeed identical, significant aspects of both the client's backent and user interface are by design very different to the web app. While the mobile app is heavy on synchronization logic (e.g. synchronization with the contacts on the user's mobile device), the web app is heavy on functionality and UI which thrives on larger screens (e.g. Covve's interactive contact network visualisation and analytics).

Iasonas's investigation tested the feasibility and desirability of homogenising all our clients onto a single PWA and experimented with some of the latest PWA technologies. We now have a clearer understanding of the art of the possible and some educated inputs into our product roadmap.

### Michael: A quick push notifications proof of concept
![firebase](/images/blog/2017-03-17-Pet-projects-day-2/firebase.png)

For a long time the team have toyed with the idea of introducing push notifications across Covve's three platforms (cross platform Android app, iOS app and web single page application). Michael's pet project conducted the preliminary research into this. He evaluated a number of SaaS offerings and implemented a quick PoC using Google's [firebase][Firebase].

Having assessed the implications we now have confidence in the effort and implications of implementing push notifications across Covve.

### Manolis: Automating the data team interface (part 1)

Covve goes to significant lengths to find updates and improvements for our users' contacts. This includes proprietary algorithms, the use of 3rd party services and our own data team.

Manolis' pet project looked at the third of these methods - automating the interface between our data team, our quality assurance team and, ultimatelly, the backend system itself. Currently relying on numerous handoffs and even (shock horror) some excel files, this process, although effective, can certainly be more efficient.

Being a two part pet project watch this space for the second part next month!

[martin]: https://martinfowler.com/
[anemic]: https://martinfowler.com/bliki/AnemicDomainModel.html
[ionic2]: http://ionic.io/2
[angular2]: https://angular.io/
[pwa]: https://developers.google.com/web/progressive-web-apps/
[firebase]: https://firebase.google.com/