---
layout: post
title:  Why I love Microservices (a PM’s perspective)
categories: Engineering
cover: /images/blog/2016-11-24-Why-I-love-Microservices-(a-PMs-perspective)/microservices.png
author: ap
redirect_from: "/Why-I-love-Microservices-(a-PMs-perspective)/"
---
[Microservices][microservices] has been a buzzword [for a while now][forawhile], and rightly so. For many products, projects and teams they provide solutions to some of the problems of large and complex software systems.

As such, when our very own Zafeiris first proposed its adoption at Covve back in 2014 (before all the hype) it felt most almost natural given our domain and approach to design. As such, Covve’s backend has been built on microservices principles virtually from day one.

Here’s a glimpse of our microservices environment as it stands today. <!--more-->Most services should be self-explanatory as they revolve around core concepts of the Covve business domain such as deduplication of contacts, syncrhonization, contact avatars, improvement of contacts, search and so on.


![Covve's Microservices](/images/blog/2016-11-24-Why-I-love-Microservices-(a-PMs-perspective)/covvems.png)

Three years later we’ve really put the microservices approach to the test and not a single day goes by that I don’t rejoice for this decision. Here’s why:

### Right techs for each service
It enables us to freely select the most appropriate technologies, frameworks and databases for each microservice, depending on its specific job. For example, the service in charge of handling avatars (images) is written in NodeJS since node works naturally with streams while the search service is written in .Net and uses Elastic Search. We are even able to mix traditional and docker deployments as well as custom built and as-a-service offerings.

A warning is necessary here though. Although microservices really help in picking any tech you want, it doesn’t mean that having multiple technologies in your production environment comes without a cost. Each stack has a learning curve, may need its own devops and CI setup and will have its own unique challenges.

### Specialisation and depth of understanding
The good news is that μS allows both specialisation and focus. Specific people can be masters of specific microservices quite easily. This goes not only for the tech involved but also the business domain and even the commercial implication where applicable.

For example, Manolis from our engineering team is, amongst other things, the master of the contacts enrichment service (the service that receives the user’s contacts and uses a multitude of methods, datasets, algorithms and external sources to enrich it with metadata such as the contact’s job or seniority). Manolis understands the business of enriching inside out, he is fully conscious of the relevant economics (especially when it comes to 3rd party sources) and is also our resident Cassandra expert.

A couple of warnings here too:

- Specialisation can quickly become synonymous to isolation and siloed behaviours. Good practices including joint design sessions and code reviews help mitigate this.
- Specialisation can also lead to key man dependencies, i.e. having parts of the system or stack that only a single person understands. Once again it comes down to good practices to make sure that this is managed.

### Rapid deployment (and easy maintenance)
Microservices allows us to confidently make small, rapid and incremental changes to our backend. We average about one release per week and as long as we remain conscious of service boundaries (and follow all the necessary good practices around testing and code quality such as high test coverage and [blue-green deployments][bluegreen]) we can release new features and optimizations with minimal risk and disruption.

Gone are the days of complex release planning, dependency mapping and whole system testing. And with them gone is the release-related stress!

### Breaking dependencies (decoupling)
Adopting the μS approach forces you to design decoupled services. Services that can be deployed independently, that can operate independently and that treat other services as 3rd parties. When designing, this puts you in a mindset which encourages resilience and forces you to break dependencies. And if you select appropriate boundaries for your services (which, mostly, are aligned to real world domain boundaries) then you’ll automatically create systems that are resilient and maintainable.

For example, the deduplication service is in charge of identifying and merging duplicate contacts. It is unaware of anything outside of its immediate remit and, in the event of its failure, the only impact on a user’s experience will be that any new duplicates will not be identified while the service is down. Every other aspect of Covve will continue to operate.

It is worth saying that sometimes breaking these dependencies is not an easy task or one that comes naturally. In some cases creating isolated services will result in compromises such as [eventual consistency][eventualconsistency] and/or duplicate denormalized data.

### Learning curve
If I take a step back and gaze at our architecture poster on the wall infront of me it is clear that Covve’s backend is large, complex and, no doubt, daunting to anyone new. If someone needed to get to know the whole (or even a large part) of the system before they can be effective it would take an induction year, not week or month.

This is both due to the tech but also due to the domain itself.

With μS, a new joiner doesn’t need to digest all this in one go. They can be very effective very quickly by focusing on a single microservice (lets say our contacts enrichment service), with little need to understand any other part of the system (or even the who business domain).

### Independent scaling
With my business hat on, this is one of my favourite benefits of the approach. Each microservice can scale independently based on whichever trigger is most appropriate for it. This allows us to scale aggressively knowing that we’re only scaling the specific part of the architecture that needs it. In other words it allows surgical injection of money (i.e. infrastructure) in very small units and at exactly the right points.

Its worth noting that this is not only a financial benefit. Knowing that scaling is zero-waste and cost-effective allows us to provide a much better user experience.

For example, the sync service is in charge of keeping our users’ contacts in sync with the various sources (such as iPhone, Exchange and Gmail). This service typically has a background role, taking care of sync in the background, without users being directly aware. However, there’s one use case where this service comes clearly to the foreground and that’s a user’s initial signup. During initial signup the sync service needs to process all of the user’s contacts as fast as possible to optimize the user’s experience. As such, the sync service has been configured to detect these special events and scale aggressively from a couple to tens of servers for just the amount of time required.

A couple of notes of caution here:

- There’s always a smallest amount of infrastructure that you will always need to run (in our case this is usually three VMs per microservice). If you break up your services into pieces that are too small then you may be left carrying a large fixed cost.
- Depending on infrastructure provider, scaling is usually not instantaneous and may take minutes (or tens of minutes, depending). If you’re using scaling to improve UX then this spin-up time may constrain the benefit.

Both of these issues are mostly mitigated by also employing docker, but that’s the topic of another blogpost!

### Troubleshooting
One of the commonly cited drawbacks of the approach is that it makes troubleshooting harder. This is because you often need to trace an issue through a number of services and understand how potentially multiple services contribute to an issue.

In our case I’m glad to say we haven’t yet come across this. Our centralized logging makes it possible to see the whole picture in one go; and ensuring that all logs carry the right IDs (e.g. userId or requestId) makes it feasible to quickly see the whole sequence of events.

### Summing up
All in all I sleep much more easily knowing that our architecture is decoupled, resilient, maintainable and cost effective. And that’s why I love microservices.

[microservices]: http://www.martinfowler.com/articles/microservices.html
[forawhile]: https://www.thoughtworks.com/insights/blog/microservices-evolutionary-architecture
[bluegreen]: http://martinfowler.com/bliki/BlueGreenDeployment.html
[eventualconsistency]: https://en.wikipedia.org/wiki/Eventual_consistency