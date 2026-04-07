---
title: "Let's Talk about Shiplap"
date: 2020-01-03 17:13:00 +0000
categories: [Hobbies, Woodworking]
tags: [woodworking, shiplap, math, joinery]
math: true
description: >-
  For the past several years of my woodworking hobby, I've been using shiplap joinery off and on. I like the look of it. I like how it can provide strength without edge-gluing. What I don't like about it - how complicated it can be to calculate any single variable.
---

For the past several years of my woodworking hobby, I've been using shiplap joinery off and on. I like the look of it. I like how it can provide strength without edge-gluing. What I don't like about it - how complicated it can be to calculate any single variable. Well - how hard it used to be. I spent a solid afternoon working through the math and came up with a simple equation.

Let $w$ be the total width of panel
Let $m$ be the number of boards in the panel
Let $n$ be the width of a single board in the panel
Let $r$ be the width of the rabbet on each board

$$ { w = m(n-r) + r } $$

Let's work an example (this happens to be for a project I'm doing right now). I need to create a back panel that is 31.5" wide out of 6 or 7 boards (the narrowest is 4.75"). I'd like to use a rabbet of 3/8". 

$$ {31.5 = 7(n - .375)+.375 } $$ 

$$ {31.5 - .375 + 2.625 = 7n } $$ 

$$ {31.5 + 2.25 = 7n } $$ 

$$ {33.75 = 7n } $$ 

$$ {n \approx 4.82 } $$

Looks like my narrowest board won't be wide enough - now I can play with the other information to see if I can get this to work without wasting material.

One limitation of this method is that it expects that all boards are the same dimension. If shiplapping a number of different width boards, it is still possible to figure out what the size of a rabbet needs to be, and it can be done by expanding the following equation out.

$$ { w = \sum_{i}^m (n_i - r) + r } $$
