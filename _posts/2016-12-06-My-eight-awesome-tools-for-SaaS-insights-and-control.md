---
layout: post
title:  My eight awesome tools for SaaS insights and control
categories: Product
cover: /images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/1.jpg
author: ap
---
Hi guys,

A quick blog post to rave about my favourite tools that help our SaaS business run efficiently and, importantly, give us the depth of understanding and analytics we need to make educated fact based decisions.

So, here goes, in rough order of awesomeness:
<!--more-->

### Kissmetrics
![Kissmetrics logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/kissmetrics.png)
[Kissmetrics][kissmetrics] is our eyes and ears on the ground. It gives us an unprecedented degree of insight into how our users use Covve and plays a central role in both our regular KPI monitoring and our roadmap decisions making process.

Unlike google analytics that provides an excellent view of aggregate data (total visits, total signups, total number of contact improvements applied), KM allows us to drill down into behaviours at an individual user level.

Here’s just a few of tens of ways we use KM:

- Funnels: Our “install to Pro subscriber” funnel has many steps. Understanding the drop off at each steps constantly allows us to identify issues and opportunities at a very micro level
- Testing hypotheses: In v3 of the iPhone app we introduced an optional two minute video highlighting Covve’s USPs. We wanted to know what percentage of people watch it and then whether watching the video has an effect on the specific features being used
- Features use monitoring: Our dashboard provides an at-a-glance view of how many users are using each of our features (e.g. contact improvements, In Touch, Leads and so on); feeding into our understanding of how Covve adds value to different types of people
- Troubleshooting: KM is invaluable when troubleshooting individual user issues as it enables us to understand exactly what actions a user has taken leading up to the issue
- KPI dashboard: Our KM dash provides real time data on all our main KPIs, instantly available and instantly insightful

### Optimizely
![Optimizely logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/optimizely.png)
We just love A/B testing, and [Optimizely][optimizely] makes it ridiculously easy to undertake experiments on our website but also on our mobile app. I won’t go on about the value (or pitfalls) of A/B testing as there’s plenty of literature on this already out there. But I do love Optimizely.

### Mandrill
![Mandrill logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/mandrill.png)
We use [Mandrill][mandrill] for system generated emails ranging from “Please confirm your email” to “You’ve been invited to join Covve by a friend”. Although Mandrill’s UI leaves a lot to be wanted, it does provide some great opportunities (which no doubt other similar services may also provide):

- A/B testing: Here we go again  Setting up A/B tests on emails takes minutes and the results are frankly eye opening
- Template changes (with no deployment needed): Changing or correcting the copy or design of templates is easy and fast

### Appsflyer
![Appsflyer logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/appsflyer.png)
[Appsflyer][appsflyer] provides a host of features which overlap with other tools we use. There is however one invaluable piece of information that, from our selection of tools, only Appsflyer provides: the ability to associate post-install behaviour to pre-install acquisition when it comes to our mobile app.

Allow me to elaborate: We use an array of advertising channels to acquire new users. All these channels go as far as reporting installs (with metrics such as cost/install). We then use Kissmetrics to understand the rest of our conversion funnels (e.g. install to user and user to Pro subscriber).

However, none of our other tools allow us to connect the two, i.e. how well do users who installed the Covve app because of a specific Facebook campaign convert to Pro.

The reason is that the action of installing an app breaks the reporting chain. Facebook (for example) tracks what happens on your browser or facebook app till the point of install. Kissmetrics only gets data once our app is installed and running.

Appsflyer, magically, transcends this boundary and can tell use which campaigns result in users that are engaged and, ultimately, revenue generating.

### Pingdom
![Pingdom logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/pingdom.png)
An elegant and simple solution to a SaaS business’ #1 fear: downtime. [Pingdom][pingdom] is easy to setup, great value for money and does everything I’d like an uptime reporting solution to do.

### GrooveHQ
![Groove logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/groove.png)
We use [Groove][groove] as our helpdesk platform. Designed for small and medium enterprises, Groove provides exactly what we need from our helpdesk solution and more; at a great price. It also provides a host of peripheral goodies which we enjoy taking advantage of (all included in the price mind you) such as a ready to go knowledge base.

### Browserstack
![Browserstack logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/browserstack.png)
When it comes to our web app ([http://app.covve.com][ourapp]), cross browser compatibility is a real concern. [Browserstack][browserstack] has helped us time and time again to test across all conceivable variations of client setup quickly and efficiently.

### Fabric / Crashlytics
![Crashlytics logo](/images/blog/2016-12-06-My-eight-awesome-tools-for-SaaS-insights-and-control/crashlytics.png)
[Crashlytics][crashlytics] iOS crash reporting. Helps us be fully aware of any and all stability issues on our iOS app, identify the root cause as well as the specific people being affected. Works well and looks cool too.

### What, no Google?
We do, of course, have [Google Analytics][google-analytics] in our arsenal. However its role is secondary to the tools already mentioned. Similarly there are a host of other tools we employ in specific scenarios (e.g. we’re currently using Crazyegg to understand scroll behaviour on our new public site) but nothing compares to the magnificent eight already set out above.

[kissmetrics]: http://jekyllrb.com/docs/home
[optimizely]: https://www.optimizely.com
[appsflyer]: https://www.appsflyer.com
[pingdom]: https://www.pingdom.com
[groove]: https://www.groovehq.com
[ourapp]: https://app.covve.com
[browserstack]: https://www.browserstack.com
[crashlytics]: http://try.crashlytics.com
[mandrill]: http://www.mandrill.com
[google-analytics]: https://www.google.com/analytics