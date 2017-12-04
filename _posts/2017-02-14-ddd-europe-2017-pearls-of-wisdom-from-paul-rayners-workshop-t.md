---
layout: post
title:  DDD Europe 2017 - Pearls of wisdom from Paul Rayner's Essential Domain-Driven Design workshop
categories: Engineering
cover: /images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/cover.jpg
author: vn
redirect_from: "/DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/"
---
Having just returned from the truly inspiring DDD Europe 2017 conference, this is a quick run-through of my experience and key pearls of wisdom I gleaned throughout, starting with Paul Rayner’s exceptional workshop on “[Essential domain-driven design][Essential domain-driven design]”.
<!--more-->

### A traveller's adventure

But first, I will start this story with a humble traveler’s endeavor. Bear with me. 

I landed in Amsterdam on Monday full of excitement for the DDD Europe conference. After a train from the airport and an underground ride from Amsterdam Central I had to figure out how to get a friend’s flat and my home for the following week. I already had a screen shot of the route on my phone:

![route](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/map.png)

Disregarding GPS technologies I decided to become an old school adventurer and go to the flat using just the picture. I walked for a few minutes full of confidence. I kept walking and after a while it became obvious that I was heading the wrong way.

Oops! It seemed so easy. How did I manage to get lost in Amsterdam? I headed towards the canal and based my navigation on the single canal of the screen shot. As you might expect canals are all over the place and I was walking towards another one. It was obvious that I didn’t know the Amsterdam domain that well. Moreover, I was reluctant to speak to any of the domain experts walking around. Luckily [Paul Rayner’s][Paul Rayner’s] workshop was starting on Tuesday and I would have a better understanding of the lay of the land until then.

### Day 1 – Essential domain driven design workshop with Paul Rayner

The first day of the Essential Domain-Driven Design workshop was about to start. All the participants were grouped in small teams. We wrote our goals of the workshop on post-it notes.

![goals](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/goals.png)

We also made a working agreement that stated how we want everyone to behave during the two day workshop. Among these rules were: “we should have fun”, “give honest feedback” and “have the right to skip an exercise or a question”.

![agreement](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/agreement.png)

Highly interactive and fun it was from the beginning! Everyone introduced themselves to someone from another table and shared their level of understanding of software design. We then got down to business.

### Good design

A good design is the one that makes adapting to the future affordable. In agile communities you hear a lot about process excellence. It’s not just about scrum masters and product owners. Agile is how you organize to do the work, but [design is the work][design is the work]!

### It’s all about business domain complexity

One of the fundamental principles is that the most significant complexity in any software project is not technical. As such, central to every software project is dealing with the business domain complexity. Consequentially, [Domain-Driven Design][Domain-Driven Design] (DDD) was created as an approach to manage software development for complex domains. DDD consists of the following parts:

![agreement](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/dddparts.png)

### Collaborative Modeling

What’s the best way to learn? Practice!

Throughout the workshop we did a case study of a concrete business example. After an initial review we tried to figure out what is important for understanding and modeling the given business domain.

The first time you read a [business story][business story] you can’t understand every concept – that’s to be expected. On the other hand, the story is memorable. It reveals key concepts for the domain and even though some aspects of the business story may seem a bit crazy, it can produce terminology and curiosity, both of which are incredibly useful.

When beginning to understand a domain, you need to wear your Sherlock hat and wonder why things are done in a certain way and what the real meaning of terms and actions is. Why is a term used here in this way and in another case in a similar but different way? Talk with people who can offer insight into the problem domain - the [domain experts][domain experts]. 

Discover the terms in the domain that describe complex concepts in a clean, concise manner. In doing so, communication’s value should not be underestimated!  Paul pretended to be a domain expert and we asked questions. From our conversation it became glaringly obvious that the questions you ask are vital. You should strive to become an [effective communicator][effective communicator]! Knowledge is gained everywhere, even in coffee breaks.

### A ubiquitous language is at the heart of good design

Ask open ended questions and walk through concrete business examples. A concrete story helps to create a shared language between technical experts and business colleagues. This is known as [ubiquitous language][ubiquitous language].

In creating the ubiquitous language, you have to make the implicit explicit! Remove terms that distract you from the problem or are [ambiguous][ambiguous]. Synonyms can be your enemy. Do “customer” and “client” have the same meaning in our domain? Deciding what a “customer” and what a “client” is can unlock key insights into the model you are building. 

The ubiquitous language developed within a team should be pervasive. It should be in tests, in code, in use cases, inside your team’s space, it should be everywhere.

### Bounded Context 

Within a team people speak using their ubiquitous language which consists of terms which are rich in domain logic. However, the same terms may have different meaning in another team. That’s why every team has its own view of the domain based on its business use cases and abstractions. Having only one model would be too rich for some and too poor for others. 

Embrace different models for different contexts (known as [bounded contexts][bounded contexts])! A “user“ in the “authentication” bounded context could be a “customer” in the “orders” bounded context and a “reviewer” in the “evaluation” bounded context. [Models need to be clear, not big][Models need to be clear, not big]!

### Creating the domain model 

From the business story and the insights you gain from the development of the ubiquitous language you can create a [domain model][domain model], which is a set of concepts expressing knowledge and rules.

A domain model represents a view of the problem domain and not necessarily the whole reality. It is useful because of its ability to represent complex logic using abstractions aimed to handle specific business use cases. Technical concerns should be isolated from domain logic! The domain model is not created once and hidden in a shelf. It needs to constantly evolve. The model should also be challenged.

### Event storming for effective model building

During our first day, Paul organized an introductory [event storming][event storming] session. It is one of the knowledge crunching techniques available for producing effective models. It is also a really fun way of doing collaborative modeling.

Event storming needs a lot of post-it notes and paper. It’s a wild west kind of thing: post first, ask questions later! People will bring different assumptions to the same problem and stick them accordingly.

Create a mess and after a lot of stickers have climbed on your wall start asking meaningful questions and put order to the chaos you created. Don’t forget to pinpoint issues and map out your ignorance! 

It’s also handy having an experienced facilitator in the event storming session. If you aren’t lucky enough to have Paul, try becoming a facilitator yourself! [Game storming][Game storming] is a book which can help you learn how to use game mechanics in your work environment for innovation and creative thinking. 

After this session, I feel each of us can read [Alberto Brandolini’s book][Alberto Brandolini’s book] and introduce event storming in our teams. I know I will give it a try! I am confident that our mini event storming sessions are still hanging proud on a wall:

![thewall](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/thewall.png)

### Tactical design

After collaborative modeling, Paul introduced us to [tactical design][tactical design].

A [value object][value object] is an object defined by its attributes, carries no concept of identity, is immutable and has side-effect free functions. On the contrary, entities have a life cycle and a unique id. If you want to learn more about them check [Paul Rayner’s blog][Paul Rayner’s blog].

![tactical](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/tactical.png)

My “a-ha” moment was that when we have a design dilemma between value objects and entities, then we should choose value objects. When you make something a value object, you simplify it. 

We applied what we learned in a code sample corresponding to our business story. We refactored the code by grouping attributes from [bloated objects][bloated objects] into higher level concepts and assigning behavior to them! Really cool!

### Day 2 – Essential domain driven design workshop with Paul Rayner

The second day started with each table’s team brainstorming questions based on the first day’s session and putting another table’s team to the test.

### The Model Exploration Whirlpool

Eric Evan’s [Model Exploration Whirlpool][Model Exploration Whirlpool] should be leveraged when guidance is needed on how to explore models: 

![whirlpool](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/whirlpool.png)

It can be a useful tool when problems are encountered during the creation of a model. One of the points made was that we should do a prototype or a proof of concept in code as soon as possible. The model is the hypothesis, the code tests it. Nonetheless, have in mind that a prototype is just an experiment and that a different mindset is required for production level code. 

### Aggregates are consistency islands

![aggregates](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/aggregates.png)

As an application grows in complexity, the number of interconnected objects can become [overwhelming][overwhelming]. [Aggregates][Aggregates] are a way to handle this complexity. They are clusters of domain objects that can be treated as a single unit.

Aggregates represent domain concepts and are a consistency boundary that ensures that the model is in a reliable state. When one aggregate is deleted, all the objects within it are also deleted. You can refer to them as consistency islands because after every transaction they are always internally consistent.

Paul presented [guidelines][guidelines] to use when choosing aggregates. Based on the aggregate design guidelines we examined different alternative design choices for our business story. In my experience, choosing aggregates can be hard, but the guidelines help. When picking an aggregate design solution it’s all about your specific use cases which act as reference scenarios. It’s OK to break the guideline if you know why, else don’t!

### Instance diagram, aggregates persistence and event sourcing

Aggregates are run-time things. Instance diagrams are informal diagrams that reflect the state of the system in a specific time, so it’s like a class diagram where the attributes have values. 
Consequently, instance diagrams as snapshots of objects in run-time are a handy tool when engaging in a conversation about aggregates with a domain expert. 

Persisting aggregates is also a really interesting topic. [Vaughn Vernon’s][Vaughn Vernon’s] books present all the different persistent options. 

Paul even presented powered up domain events in [event sourcing][event sourcing]. In event sourcing, instead of saving the current state of the object, you save the events that lead to the current state. A really interesting talk you can check out is [Greg Young’s in DDD Europe 2016][Greg Young’s in DDD Europe 2016].

### Strategic patterns

In such a dynamic workshop every table’s team researched and presented a [strategic pattern][strategic pattern]. While public speaking can be terrifying, in the creative environment created by our host it was a really fun experience sharing our understanding of a strategic pattern we just read about.

![conformist](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/conformist.png)

### Context Map

DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships. Doing a context map reveals the different bounded contexts: 

![contextmap](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/contextmap.png)

### Core Domain

Last but not least, we clarified what a [core domain][core domain] is. It’s kind of the secret sauce that differentiates your company from others. We should determine which parts of the domain constitute [the core domain][the core domain]. It’s the perfect place for applying DDD! Note that the core domain may change over time. 

Remember that [non-core domains][non-core domains] should not be over engineered. Generic domains may be purchased as third party tools or outsourced. Supporting domains could be handled from junior developers. 

![domains](/images/blog/2017-02-14-DDD-Europe-2017-Pearls-of-wisdom-from-Paul-Rayners-workshop/domains.png)

### Wrapping up

Overall the workshop was an amazing experience! I would recommend it both to DDD newbies and to people who know DDD parts but are not clear on the whole picture. Paul Rayner is a great facilitator, can communicate hard to grasp DDD concepts with ease, while creating a fun and challenging environment for all the participants. Upon enjoying a few drinks on the following days, Paul even suggested ways to [improve our memory][improve our memory]. Cheers to that!

[Essential domain-driven design]: https://dddeurope.com/2017/speakers/paul-rayner/
[improve our memory]: https://www.amazon.com/Moonwalking-Einstein-Science-Remembering-Everything/dp/0143120530
[non-core domains]: https://content.pivotal.io/blog/getting-started-with-domain-driven-design-top-3-concepts
[the core domain]: https://www.infoq.com/presentations/strategic-design-evans
[core domain]: http://blog.jonathanoliver.com/ddd-strategic-design-core-supporting-and-generic-subdomains/
[strategic pattern]: http://gorodinski.com/blog/2013/03/11/the-two-sides-of-domain-driven-design/
[Greg Young’s in DDD Europe 2016]: https://www.youtube.com/watch?v=LDW0QWie21s
[event sourcing]: https://goodenoughsoftware.net/tag/event-sourcing/
[Vaughn Vernon’s]: https://vaughnvernon.co/?page_id=168
[guidelines]: https://vaughnvernon.co/?p=838
[Aggregates]: http://thepaulrayner.com/blog/aggregates-and-entities-in-domain-driven-design/
[overwhelming]: http://culttt.com/2014/12/17/aggregates-domain-driven-design/
[Model Exploration Whirlpool]: http://domainlanguage.com/ddd/whirlpool/
[bloated objects]: https://martinfowler.com/bliki/AnemicDomainModel.html
[Paul Rayner’s blog]: http://thepaulrayner.com/archive.html
[value object]: https://lostechies.com/jimmybogard/2008/05/21/entities-value-objects-aggregates-and-roots/
[tactical design]: http://gorodinski.com/blog/2013/03/11/the-two-sides-of-domain-driven-design/
[Alberto Brandolini’s book]: http://eventstorming.com/
[Game storming]: http://gamestorming.com/
[event storming]: http://ziobrando.blogspot.gr/2013/11/introducing-event-storming.html
[domain model]: http://culttt.com/2014/11/12/domain-model-domain-driven-design/
[Models need to be clear, not big]: https://www.youtube.com/watch?v=yPvef9R3k-M
[bounded contexts]: https://martinfowler.com/bliki/BoundedContext.html
[ambiguous]: http://www.jamesshore.com/Agile-Book/ubiquitous_language.html
[ubiquitous language]: https://martinfowler.com/bliki/UbiquitousLanguage.html
[effective communicator]: https://www.youtube.com/watch?v=XYw5Mn5yVMM
[domain experts]: http://www.informit.com/articles/article.aspx?p=1944876
[business story]: http://thepaulrayner.com/blog/2013/02/15/agile-user-stories-and-domain-driven-design-ddd/
[Domain-Driven Design]: https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215
[design is the work]: https://www.youtube.com/watch?v=Bl30X0MvT0I
[Paul Rayner’s]: http://thepaulrayner.com/about/