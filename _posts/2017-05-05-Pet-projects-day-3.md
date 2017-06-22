---
layout: post
title:  Pet project day - April 17 - Watson, chatbots, event stores and cross platform dev ops
categories: Engineering
cover: /images/blog/2017-05-05-Pet-projects-day-3/petproject.png
author: ap
---
The last Friday of each month is Pet Project day over here at Covve. Giving ourselves the time to experiment with new and exciting technologies, try out new approaches or just scratch that technological itch.

April's pet projects included a bottom up review of cross platform devops, and experimentation with Watson and event sourcing.
<!--more-->

### Iasonas: Cross platform app devops

![DevOps](/images/blog/2017-05-05-Pet-projects-day-3/devops.jpg)

Our Ionic/Angular devops setup allows us to rapidly and confidently release new features and updates. Manual steps are all but eliminated, code reviews and automatic testing are an integral part of the process and other tasks such as linting are part of every build. Continuous integration at its best.


And yet, to achieve this, our setup contains many underlying technologies that require deligent setup and fine tuning. In an attempt to 
thoroughly understand the various components of our code infrastructure I did a bottom-up review of the whole stack and focused on the following topics.
- [npm][npm scripts] vs [grunt][grunt] vs [gulp][gulp]. All these are used as task runners that do tasks such as running tests and linting your code. npm scripts are the popular pick here
- [webpack][webpack] vs [browserify][browserify], as a means to bundle js files for browsers
- transpiling (turning our typescript into es6 code into es5 which is compliant in all browsers)
- polyfilling (what can't be transpiled, is polyfilled with "emulations" of the real thing)
- dealing with features that can't be polyfilled or transpiled like service workers and push APIs
- setup and config typescript projects from 0, learn about typescripts various compiler options
- attempt to scaffold a typescript project with a generator like [yeoman][yeoman]

### Andy: Event sourcing

Event sourcing is an approach whereby events are a primary citizen of the system (a role usually given to the data source itself). All events ever created are permanently stored and can be replayed in order to calculate today's state.

Lets take a classic online bookstore as an example. And lets say that our user added 3 products to the basket, then removed one and then submitted their order. In a traditional model we'd be storing the entity called "order" which would include two items. The information about the removal of the third item would not be captures. In an event sourcing world we'd be storing the five actions that led to this final state, i.e. add item, add item, add item, remove item, submit order.

Adopting this approach can provide some interesting opportunities. My two favourites are:
- No information loss. Not only does this provide an excellent audit trail but it also provides an absolute treasure trove of data for use in yet-to-be-thought-of analyses
- The ability to rewind time, see the state of the entire system at a particular point in time and then replay history. Even more interestingly, you could change the system (e.g. tweak an algorithm) and then replay all events and see what impact this change would have had, had it been applied in the past!

For more on event sourcing check out [http://docs.geteventstore.com/introduction/4.0.0/event-sourcing-basics/]

### Zafeiris: Watson

AI is of course all the rage these days. At Covve we've been using machine learning technique for a while now with good results. Zaf undertook to play around with one of the most popular AI's out there and identify potential opportunities for us.

A pet project day later - we now understand a lot more about what [Watson] can do and gave even identified a couple of implementations which provide an excellent fit with our business and our product. However, the next big question is value for money... and that's where trouble may lie...

### Manolis: Build Stuff conference (Majorca)

![BuildStuff](/images/blog/2017-05-05-Pet-projects-day-3/buildstuff.jpg)

In case you're wondering what Manolis was up to this pet project day... he was attending the [buildstuff][Build Stuff] conference in Majorca. We are not jealous at all.

[Watson]: https://www.ibm.com/watson/
[http://docs.geteventstore.com/introduction/4.0.0/event-sourcing-basics/]: http://docs.geteventstore.com/introduction/4.0.0/event-sourcing-basics/
[npm]: https://docs.npmjs.com/misc/scripts
[buildstuff]: http://buildstuff.lt/summer/
[grunt]: https://gruntjs.com/
[gulp]: http://gulpjs.com/
[webpack]: https://webpack.github.io/
[browserify]: http://browserify.org/
[yeoman]: http://yeoman.io/