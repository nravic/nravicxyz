---
title: "Solving Non Planar Two-Link Systems"
date: 2018-10-12T01:02:30+04:00
draft: false
---

One of the things I'm working on at the [ADAMS](http://adams.eng.buffalo.edu/) lab at SUNY Buffalo is designing a miniature insect-inspired hexapod from the ground up, developing a controls architecture using neuroevolution algorithms written in-house to actually building it (eventually) with smart material actuators. 

Approaching the problem head on with a dynamic analysis fails, because the joints of the leg in my system are coupled. It fails more because I thought it was tedious and a waste of my time; I'm sure with enough determination you could work around it. A post-doc at the lab suggested inverse kinematics. Most literature I found had direct solutions to simple planar two-link systems; which proved useless. I couldn't solve it directly (or the classical way), and instead opted for using [Denavit-Hartenberg parameters](https://www.wikiwand.com/en/Denavit%E2%80%93Hartenberg_parameters), the resulting equations of which are used to solve for joint angles. 

I previously compiled the derivation in LaTeX, and can't really figure out a simple way to render LaTeX in Hugo without spending a ridiculous amount of time on it. They're shown below as pngs.

![dh1](/img/dh-0.png)
![dh2](/img/dh-1.png)





