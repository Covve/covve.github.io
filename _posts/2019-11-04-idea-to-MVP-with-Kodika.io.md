---
layout: post
title:  From idea to MVP in 4 days with Kodika.io
categories: Engineering
cover: /images/blog/2019-11-04-idea-to-MVP-with-Kodika.io/cover.jpg
author: ap	
---
Its pet projects day at Covve, a time when ideas are born and innovation flourishes. This particular Friday an interesting debate was underway… Given the investment and exceptional results of building Covve’s business card scanning engine (hint: one of the world’s most accurate engines which is also language agnostic), wouldn’t it be great to make this available to people through a standalone app? 

This is a debate we’ve often had at Covve HQ and the hypothesis is solid – there’s an entire audience out there who want a dedicated, simple and super accurate scanner. We’ve already developed the tech so why not make it?

The answer regrettably has always been that 100% of the team’s effort must go to Covve and side-projects like this, no matter how tempting, must take second priority.
… that is until [Kodika] came along.

<!--more-->

Kodika is a really new service which lets you build iPhone apps with simple drag and drop (a “wordpress for apps”), making the journey from design to app store a matter of hours and days (not weeks and months). Indeed, four days later our pet project hypothesis was live on the app store and making a splash (check out [Covve Scan])!


![whatsthepoint](/images/blog/2019-11-04-idea-to-MVP-with-Kodika.io/appstore.jpg)


So, Kodika delivered on its promise. However what I didn’t expect was the quality of the code coming out of it. It was absolutely production-level: it is robust, it is limitless (if you can code it traditionally, you can Kodika it too) and is performant. So much so actually, that what started as a proof of concept has now been live for the best part of 2019 and has amassed 234 ratings with an average of 4.9 stars – not too shoddy for a 4 day pet project!

![whatsthepoint](/images/blog/2019-11-04-idea-to-MVP-with-Kodika.io/ratings2.jpg)

### The process was quite simple
- We imported our designs from Zeplin.io into Kodika with one click. UI – done :)
- We built all the business logic we wanted using that [funky blocks drag and drop interface] without having to compromise on anything which was great
- We built the necessary API calls for integrating with our backend (i.e. the scanning engine) but also 3rd party services (we use Kissmetrics for our analytics)
- We then found our ideal plugin for helping users photograph the business card. We chose a great plugin provided by WeTransfer. For this we did need to get in touch with the Kodika team as it isn’t provided out of the box. The team was refreshingly responsive and got us up and running in no time. We were also told that going forwards plugins like this will be available on the Kodika marketplace
- We then added some native components (e.g. adding the native share functionality was literally one line of code)
- Finally, we wanted to be able to generate some revenue from the project so we needed to add payment support. Once again we had to get in touch with the Kodika guys who added us to their payments Beta
- Launch, sit back and enjoy :)


![whatsthepoint](/images/blog/2019-11-04-idea-to-MVP-with-Kodika.io/code.jpg)

### What I liked
- **Speed:** Kodika enabled us to go from design to live product many times faster than traditional app development
- **Full-featured:** We didn’t have to make any compromises in terms of features, integrations or business logic
- **Production-ready:** The generated app was as robust and performant as a traditional app
- **Blurring the lines:** Due to its intuitive interface, Kodika can be easily used by anyone. This meant that the lines between design and development become even more blurred, with our design lead making changes directly in Kodika


![whatsthepoint](/images/blog/2019-11-04-idea-to-MVP-with-Kodika.io/export.jpg)

### What I’d like to see in the future
- **Mac app:** If today’s iPad Kodika helps you develop at light speed, Kodika on the Mac will up it to ludicrous speed! Apparently we can expect this later this year.
- **More plugins please:** It was great having direct contact with the Kodika team for matters such as plugins and payment but I’d certainly like to see the promised Kodika Marketplace for quick access to plugins
- **Source control:** Kodika is, surprisingly, great for teams of people working on the same project as everyone is working on the same "live" files. However, the larger the project the more important it is to have some kind of source control, versioning etc. It seems the Kodika guys are planning to include this too which will make my day


![whatsthepoint](/images/blog/2019-11-04-idea-to-MVP-with-Kodika.io/upgrade.jpg)

### OK, so should we fire our engineering team?
Well, not quite. Kodika is great but isn’t for every type of project. Kodika is best when the effort of the app in question is mostly the interface and API calls to your backend. On the other hand if the app needs to contain significant portions of custom code, processing and heavy logic then stick with traditional engineering.

So, **TLDR**: if you’re starting an app dev project now, seriously consider Kodika either for its proof of concept or even for the full blown thing. It certainly worked for us!

[Kodika]: https://kodika.io
[Covve Scan]: https://covve.com/cardscanner
