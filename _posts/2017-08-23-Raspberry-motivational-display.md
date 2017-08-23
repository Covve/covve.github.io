---
layout: post
title:  Raspberry Pi KPI & motivation board
categories: Team
cover: /images/blog/2017-08-23-Raspberry-motivational-display/cover.png
author: ap	
---
"Always code as if the guy who ends up maintaining your code is a violent psychopath who knows where you live". It's motivational messages like this that keep the Covve engineering team operating at peak efficiency. They are delivered 24/7 by our homemade Raspberry powered LED matrix display and are accompanied by live values of our main KPIs (arguably the primary purpose of the device).
<!--more-->

The idea for some kind of key performance indicator display had been brewing for a while in the Covve offices. One day an old Raspberry had appeared on one of the desks... then, some weeks later, an 80x8 LED matrix display and one thing led to another.

The project ended up involving almost the entire team at one point or other and ended up delivering both a stylish (if we can say so ourselves) and useful gadget. It lights up one of the engineering rooms with real time updates on our key metrics and also intersperses motivational messages from time to time.

### Details of the build

![insides](/images/blog/2017-08-23-Raspberry-motivational-display/pi.JPG)

A quick runthrough of the main components of the build:

1) At the heart of the display is a Raspberry Pi 2. The first incarnation of the display used a Pi 1 but the display frequently experienced flickering so an upgrade was in order. We're running Raspbian on this

2) The 80x8 LED matrix display itself. You can find details [here][here]. We also used external power (a 12v transformer from an old mobile phone did the trick)

3) Connecting the two together needs A LOT of patience and attention to detail. You'll need to match the pinout from the LED matrix datasheet to the [pinout of the Raspberry's port][pinout of the Raspberry's port]. You can check out [Pete Gross' pin connection diagram][Pete Gross' pin connection diagram] for details.

4) For driving the display from the Raspberry we adapted [Pete Gross'] driver. You can [download our adaptation][download our adaptation]

5) We made a small programme to fetch the KPI data from Covve's servers, display it on the display and also interplay the messages amongst the stats

6) Designed and built the Plexiglas enclosure


And that's it. [Check it out in action][Check it out in action]

[here]: https://www.embeddedadventures.com/datasheets/LDP-8008.pdf
[pinout of the Raspberry's port]: https://pinout.xyz/pinout/pin4_5v_power
[download our adaptation]: https://github.com/masimplo/python-ldp8008
[Check it out in action]: https://vimeo.com/230752600
[Pete Gross' pin connection diagram]: http://www.embeddedadventures.com/Tutorials/tutorials_detail/184