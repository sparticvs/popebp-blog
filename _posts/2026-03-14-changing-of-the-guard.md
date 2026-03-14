---
title: Changing o' the Guard
date: 14 March 2026
tags:
    - random
---

I've been so very inconsistent updating this blog. I kept telling myself that
this time it will be different and that I will update more! Let's face the
facts, that's not really happening anytime soon. So instead, no promises this
time.

I'm migrating systems again. It seems that's probably more of what this blog is
about than anything else. No one really cares all that much about those issues.
In fact, more often than not, it's just purely me capturing some history or
technical knowledge so that when things break, I can go back and look at how I
changed this so I can get the system back up and running.

I've been hosting this blog for more than a decade on my own hardware. My
original domain was 'pushesp.net' or something like that, and when I really got
further into vulnerability analysis and penetration testing work at my first
job, I found myself writing exploits so much, that I realized that the name of
the blog was wrong.

For the unaware, 'pushesp.net' was a reference to the Intel x86 instruction
`push %esp` which effectively was the instruction to store the extendend stack
pointer on the stack in preparation for a new context. When I started getting
into return-oriented programming (ROP) attacks as my bread and butter at work,
I realized it should be 'pop %ebp' instead, since that is where the chaos
really starts. When the attacker can control the `ebp` register, you are
controlling a lot of the system. Honestly, `eip` is better, as it's the
instruction pointer, but someone had beat me to that domain, so `ebp` had to
suffice.

All that said, it served me well, despite the uninitiated referring to the site
as 'Pope BP'... as if I was the Catholic Bishop of Roman Oil. I always
corrected them and I was fine with it since I got to nerd out for a bit about
this very topic.

Anyway, long post short, I'm going to do the thing that I thought about doing
when GitHub came out originally, just use GitHub as the blog. So here we are.

I'll be moving posts over from my old Ghost system and rely on a more reliable
hosting of GitHub Pages. Maybe I'll use this to document my journey of moving
off the old stack and setting it up as a Kubernetes playground.

All that said, maybe I'll add a confession here. Working on blogs have been
mentally exhausting for me. I'm a bit of a perfectionist, AuDHD being what it
is and all, and so I have probably a dozen or so half written articles that
never were published because I kept trying to find the *right* way to say what
I wanted instead of just saying it and then maybe getting some questions. As
part of my move to GitHub Pages, and in the advent of AI, I'm incorporating
Claude into my post regime. Claude's role will be limited to SEO, organization,
and probably some editorial proofing. I tend to ramble, and while I feel like
all this context is necessary (*cough* AuDHD *cough*) it's probably not.

Any who... stay frosty friends.
