---
title: Mandatory Encryption on XMPP Will Not Work*
date: Mar 23, 2017
tags:
  - security
---
*Originally published on [Medium](https://medium.com/@sparticvs/mandatory-encryption-on-xmpp-will-not-work-2dfb2e11c586#.as0bvcyt7), some content differs*

\* *- At least not how Peter Saint-Andre is recommending*

If you haven’t seen the article as to which this post is referencing, check out [Mandatory encryption on XMPP starts today](https://web.archive.org/web/20230320153126/http://blog.prosody.im/mandatory-encryption-on-xmpp-starts-today/) by the Prosody Team.

Today is considered to be the day that every XMPP provider (XMPP is the messaging protocol nearly everyone uses; Facebook, AOL, etc.) needs to enforce encryption. Unfortunately, XMPP’s design never really introduced a secure way to begin encryption. Other unofficial ideas were suggested, like XMPP(S) and S-XMPP, but they both required a proxy that would immediately start a SSL/TLS tunnel for the users. However, doing it this way is what experts (myself included) have called **hard to do right.** Why? Simple, you have to enforce certificate validation. OpenSSL, which was once widely respected, had a hard time of doing that correctly. Web browsers have an issue doing it correctly. It is easy to mess up, especially when most engineers are focused on meeting deadlines, budgets, and impossible demo timelines. Insecure prototypes become the final product because someone in Business Development already sold 50 licenses because they are under pressure to make sales.

## Why do I know this, and why do you trust me?
I have been down this road. I lead the security design for the IM solution that my previous employer worked up. Before I looked at the code, they were already slated to ship on an impossible timeline. Once I required the encryption methods to change, everyone went crazy because it was the week before shipping. The encryption was being done the wrong way. The way that is specified in the XMPP Specification; "STARTTLS."

STARTTLS is the single worst method for doing TLS. Why? Because it is so damn easy to proxy the connection and strip TLS (using a tool like "stripssl") right off of the stream allowing everyone to see the data. This is a terrible design, and researchers have already pointed out this flaw several times. The target they used was Google’s GChat, and suffice it to say, it isn’t around anymore.

## How do we do it correctly then?
Now that is a good question to ask. Ideally, you stay far, far, far away from *STARTTLS*. Again its not the best design and its easy to get crypto stripped off and the work-around to protect against it is annoying at best. So the *ideal* way is to actually do something very simple, use a SSL/TLS tunnel to start with and write your client to actually enforce the proper TLS certificate. Much in the way that Google has Chrome enforce their certificate. That would really only leave two types of people to be able to crack the stream, those that never changed their Private Keys after Heartbleed and those that work for ~~the US Government~~ a nation-state.

