---
layout: post
title:  How we reduced Azure costs by 33%
categories: Engineering
cover: /images/blog/2017-04-21-How-we-reduced-Azure-costs-by-33pc/pricing.png
author: ap
redirect_from: "/How-we-reduced-Azure-costs-by-33pc/"
---
With cloud services it is quite easy for costs to incrementally increase without any alarm bells going off. Increases tend to be small and can often happen automatically (e.g. due to changes in volumes or changes in unit pricing). As such it is good practice to monitor and challenge cloud costs on a regular basis.

Our recent audit of our Azure cost enabled us to reduce our monthly bill by 33%. Here are the main ways we achieved this.
<!--more-->

### Review pricing and identify equivalents
![a1 machines](/images/blog/2017-04-21-How-we-reduced-Azure-costs-by-33pc/a1v2.png)

Azure’s services change rapidly and so does its pricing. What is interesting is that in a bid to push customers to newer types of infrastructure (and off older types), Azure will often charge less for the newer and better variants of their services.

For example, the old A1 windows cloud service has 1.75GB of RAM and costs €50.19 per month. The new A1v2 sports 2GB of RAM, a processor that is allegedly 30% faster and costs €38.90 per month.

Switching from one type to another is, in most cases, a matter of minutes (assuming your devops is up to scratch). So, getting friendly with [Azure's pricing calculator][apc] definitelly pays off.

### Review scaling rules
![azure scaling](/images/blog/2017-04-21-How-we-reduced-Azure-costs-by-33pc/scaling.png)

Covve is architected as a collection of microservices, with each microservice configured to scale independently based on whichever metric is most appropriate (e.g. CPU load or queue size).

Regular review of these scaling rules can provide opportunities for optimization. The new Azure portal provides some new analytics that provide a deeper look into how each service has been scaling as well as the average number of instances.

Our review identified some services that were idling at more instances than necessary and some that were scaling out prematurely, both of which were good opportunities to reduce cost.

### Identify performance hotspots

By looking at the performance of a microservice over the course of a whole month it is possible to identify unexpected patterns and insights. These may be good triggers for a closer look at the design and code of the microservices.

For example, one of Covve’s microservices generates periodic automatic emails and notifications. This was considered a lightweight microservice which idles at just one A1 machine and scales three times a day for a short period when running bulk jobs.

And yet, review of the average number of instances throughout the month revealed that actually this service averaged 6 servers and cost a lot more than anticipated. This led to a deeper review of the service, rapid optimization of the codebase and deployment of an update to remove the necessity to scale out during the bulk jobs.


### Auto-switch off unused machines

It is likely that the estate includes machines which used rarely and for specific purposes. For example, these may relate to devops or migration activities. It may be acceptable for these machines to generally remain shut down and be started up manually when required.

Azure provides scheduling functionality to auto-shut down machines in case they are left on, making such machines cost a fraction of what they used to.


Finally it is worth saying that these kinds of reviews do not negate the need for good planning, good system design and attention to performance and resources during the development lifecycle. But a periodic audit can certainly unearth some hidden gems.

[apc]: https://azure.microsoft.com/en-us/pricing/calculator/