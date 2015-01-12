---
layout: post
title:  "Basic Gameplay, Kickback, Lamp Issues, and Magnet Timings"
date:   2015-01-06 23:56:00
categories: news
tags:
---

Had a workday on Saturday to get down some basic gameplay features that we need
to get working.  Mike and Ken showed up to compare software testing with the real
deal.

Hooked up the P-ROC, and it only took us two times to get things up and running.
Sound was fully working (through the laptop).

![Jon doing some testing]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/jonTesting.jpg)

Our first goal was to plunge a ball.  This worked as expected, but we ran int our
first gameplay problem, as no fear launches the ball into a subway.  This was
corrected and we moved onto the kickback.

This didn't turn out to be a problem at all since the table is designed such that
if the solenoid is fired when the switch is triggered, the ball will properly be
plunged back onto the playfield.

The kickback was trivial.  The magnets were not.  We played around with various
solenoid "pulse" timings, but none of them worked.  It was random weather the
ball would fly all the way around or be grabbed by the magnet and flung back down
the ramp.

We did find a good timing for ball rejection.  A solenoid pulse of 70ms on any
of the magnets throws the ball back down the ramp.  This will be incorporated
into the rules in the future.

While watching Pinball Done Quick, part of Awesome Games Done Quick 2015, I was
able to do some magnet testing.

![Logic setup]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/logicFar.jpg)

Probes were attached to the optos and to the U5 decoder chip which activates the magnets.

![Logic closeup]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/logicClose.jpg)

As shown below, so long as the switch is on, the magnet is on.  The ball
passing the switch activates the magnet (as along as the ball is in front of the
switch).  The first picture is a normal up-the-ramp shot, while the second picture
is the ball falling back down the ramp.

![normal magnet activity up the ramp]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/magnetall.png)

![ball falling back down the ramp]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/fallDown.png)

A close up of the first switch activation shows that the magnet actually pulses
during the "on" time (and ends when the switch goes HIGH again).  This shows us that doing the solenoid "pulse" is the
incorrect solution.

![single magnet activation]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/magnetSingle.png)

If we look at the pulse up close, we can see that it's about 1ms, or at least close
enough to 1ms for government work.

![zoom in on the magnet pulsing]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/magnetZoom.png)

We will do more testing and make sure this works, but this problem now seems to
be solved.

As a quick last test, I tested the left wireform magnet diverter.  This has the second
magnet hold the ball for a little bit and then drops it to the left wireform.  As
shown below, this is more like the "pulse" of the solenoid, but about 80ms rather
than the standard 30ms.

![ramp in left wireform divert mode]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/grabAndHold.png)

![zoom in on the second magnet holding the ball]({{ site.url }}/assets/article_images/2015-01-06-basic_gameplay/grabAndHoldZoom.png)

This can be implemented by calling a standard soleniod pulse for 80ms.

We tried some lamp tests, but the lamps appeared dim.  The more lamps we light
at once, the dimmer they are.  We found no immediate reason for this, and we will
need to do more real-world testing and compare how our lamps work to the normal game
since the lamps function correctly there.

We have plenty to work on.  Ken is implementing what is, right now, the talking
skull, while the rest of us need to put together a basic ruleset.  Likely some
speedrun type stuff in honor of Pinball Done Quick.  We are hoping for some more gameplay
music, and are looking to get at least one basic animation in the near future.
