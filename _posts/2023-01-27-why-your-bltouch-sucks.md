---
title: "Why Your BLTouch Sucks..."
date: 2023-01-27 00:00:00 -0400
categories: [Hobbies, 3D Printing]
tags: [3d-printing, creality, ender-3, bltouch, crtouch]
description: >-
  Why the CRTouch or BLTouch might not seem to be working on your 3D printer, and how a simple Cura GCode update can fix it.
---

I've recently got into 3D Printing and immediately out of the gate, I bought a CRTouch (Creality's version of the BLTouch) for my Creality Ender 3 v2. I have a lot of experience with tuning my woodworking tools, and tramming (aka bed leveling) the bed was pretty solid after I was done. My biggest complaint would just be that the plate glass that was shipped for the printer is far from flat, which just implies a poor quality in my book, so I was glad I bought the CRTouch to "fix its flatness" in software. However, I didn't see any improvement when I did calibration tests afterwards. 

It wasn't until I started reading the Marlin GCode manual did I start to find some information I didn't expect, which led me down a YouTube trail and ended with...I needed to update my printer configuration in Cura. I have since added `M420 S1 Z0` (Marlin FW specific by the way) as a line immediately following `G28`, and I couldn't be happier with the results. 

It amazes me that neither Creality documentation nor YouTube tutorials for installing the BLTouch that I watched ever mentioned this, so if you find your prints are just a bit off and/or you are having bed adhesion issues on the glass, maybe you aren't actually getting benefit of your bed leveling probe.

```text
M420 S1 Z0
```

```text
G28
```
