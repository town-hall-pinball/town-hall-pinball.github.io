---
layout: post
title:  "3D vs 2D Rendering"
date:   2014-10-25 12:11:00
categories: news
tags:
---

While putting together the basic attract mode, I noticed that the transition that scrolls the "NO FEAR" title from the bottom of the frame didn't always work. Sometimes it would scroll correctly, other times it would simply pop up in the center. When we testing on the Twilight Zone machine, I never saw that on the real dot-matrix display so I assumed it was just an issue with rendering in the development display.

This became problematic when trying to implement an animated gradient test as seen here:

<iframe width="560" height="315" src="//www.youtube.com/embed/uvzsjozD4NM" frameborder="0" allowfullscreen></iframe>

As you can see, it freezes up every now and then. I tracked this down to the rendering function that draws the frame.

The pyprocgame library has two different ways the DMD can be rendered. It prefers to use pyglet and renders using OpenGL. I'm not sure why it was so, and I am not an OpenGL expert. I forced it to use the fallback 2D rendering with pygame and that was smooth. The implementation appeared to be incomplete as it looked boring, one pixel per dot, all white, and the scale factor was hard-coded. I made the dots bigger and orange, and here is the result:

<iframe width="560" height="315" src="//www.youtube.com/embed/f0TljaRGt3Y" frameborder="0" allowfullscreen></iframe>

I'm not sure why pyglet was chosen over pygame. Maybe we will find out later.
