---
layout: post
title:  Pet project day - Feb 17 - Anti-patterns, PWA and push notifications
categories: Engineering
cover: /images/blog/2017-03-17-Pet-projects-day-2/petproject.png
author: ap
---
The last Friday of each month is Pet Project day over here at Covve. Giving ourselves the time to experiment with new and exciting technologies, try out new approaches or just scratch that technological itch.

February’s pet projects ranged from an experimentation with progressive web apps to putting our code's deisgn to test against Martin Fowler's personal pet hate, the anemic model anti-pattern.
<!--more-->

### Andy and Zafeiris: The anemic domain model anti-pattern (a cost/benefit analysis)

![AnemicModel](/images/blog/2017-03-17-Pet-projects-day-2/anemicmodel.png)

Discussions into correct design, use of patterns and maintainable and future proof code are quite common around the water cooler. 

So, with a statement as powerful as the above, from an authority as credible as [Martin Fowler][martin], Zafeiris and Andy just couldn't resist joining forces and putting our code to the test.

[Anemic models][anemic], in Martin's words, are objects which, when you look at their behavior, you realize that there is hardly any behavior on them, making them little more than bags of getters and setters. They're considered an anti-pattern because they incur all of the costs of a domain model, without yielding any of the benefits.

This pet project searched for occurences of this anti-pattern in the codebase of our cross-platform app and evaluated both why they came about and the implications (both cost and benefit) of addressing them.

More importantly it established an agreed approach for dealing with such occurences going forwards.

### Iasonas: Experimenting with progressive web apps

![pwa](/images/blog/2017-03-17-Pet-projects-day-2/pwa.png)

Iasonas is the newest member of the cross-platform (XP) team, focused these days on the [Ionic 2][ionic2] and [Angular 2][Angular2] aspects of Covve's next generation app. The XP app is currently in production on Android and is planned to replace the existing native iOS app in due course.

The Covve cross platform app runs across devices (android, iphone, web) and already meets (or could be made to meet) the definition of a [Progressive Web App][pwa] (PWA), namely:

"Progressive Web Apps are user experiences that have the reach of the web, and are:
- Reliable - Load instantly and never show the downasaur, even in uncertain network conditions.
- Fast - Respond quickly to user interactions with silky smooth animations and no janky scrolling.
- Engaging - Feel like a natural app on the device, with an immersive user experience."

Or, bypassing some of the high level fluff, a [fuller definition][fullerdef] would be:
- Progressive - Works for every user, regardless of browser choice because it's built with progressive enhancement as a core tenet.
- Responsive - Fits any form factor: desktop, mobile, tablet, or whatever is next.
- Connectivity independent - Enhanced with service workers to work offline or on low-quality networks.
- App-like - Feels like an app, because the app shell model separates the application functionality from application content .
- Fresh - Always up-to-date thanks to the service worker update process.
- Safe - Served via HTTPS to prevent snooping and to ensure content hasn't been tampered with.
- Discoverable - Is identifiable as an "application" thanks to W3C manifest and service worker registration scope, allowing search engines to find it.
- Re-engageable - Makes re-engagement easy through features like push notifications.
- Installable - Allows users to add apps they find most useful to their home screen without the hassle of an app store.
- Linkable - Easily share the application via URL, does not require complex installation.

However, on further analysis there are two main reasons that make it undesirable for us to consolidate our mobile and and our web app despite the significant degree of commonality between them:
a) Although the business domain is indeed identical, the Covve mobile app provides, by design, a very different feature set and experience to the web app - in essense the two apps are complementary. For example, the focal point of the web app is the interactive mapping and analytics of the user's contact network which necessitates larger screens. The mobile app does not have this feature but is instead heavier on comms-related features such as logging each call made and enabling the user to take notes against it. So, the two apps are by design different in their features and behaviour.
b) A fundamental part of the Covve mobile app is synchronization with the user's device address book. This is not [currently supported by PWAs][pwafeatures].

In summary, Iasonas's investigation tested the feasibility and desirability of homogenising all our clients onto a single PWA and experimented with some of the latest PWA technologies. We now have a clearer understanding of the art of the possible and some educated inputs into our product roadmap. We we also continue to monitor this space with interest.

### Michael: A quick push notifications proof of concept
![firebase](/images/blog/2017-03-17-Pet-projects-day-2/firebase.png)

For a long time the team have toyed with the idea of introducing push notifications across Covve's three platforms (cross platform Android app, iOS app and web single page application). Michael's pet project conducted the preliminary research into this. He evaluated a number of SaaS offerings and implemented a quick PoC using Google's [Firebase][firebase].

Having assessed the implications we now have confidence in the effort and implications of implementing push notifications across Covve.

### Manolis: Automating the data team interface (part 1)

Covve goes to significant lengths to find updates and improvements for our users' contacts. This includes proprietary algorithms, the use of 3rd party services and our own data team.

Manolis' pet project looked at the third of these methods - automating the interface between our data team, our quality assurance team and, ultimatelly, the backend system itself. Currently relying on numerous handoffs and even (shock horror) some excel files, this process, although effective, can certainly be more efficient.

Being a two part pet project watch this space for the second part next month!

[pwafeatures]: https://whatwebcando.today/
[fullerdef]: https://developers.google.com/web/fundamentals/getting-started/codelabs/your-first-pwapp/
[martin]: https://martinfowler.com/
[anemic]: https://martinfowler.com/bliki/AnemicDomainModel.html
[ionic2]: http://ionic.io/2
[angular2]: https://angular.io/
[pwa]: https://developers.google.com/web/progressive-web-apps/
[firebase]: https://firebase.google.com/