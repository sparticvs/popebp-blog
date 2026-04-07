---
title: "Defining Non-Repudiation"
date: 2022-01-28 00:00:00 -0400
categories: [Security]
tags: [security, nist, authentication, non-repudiation]
description: >-
  It All Started with a Disagreement. The other day I was in a workshop when the definition of non-repudiation was stated and I was left confused...
---

## It All Started with a Disagreement

The other day I was in a workshop when the definition of non-repudiation was stated and I was left confused. It's not that I don't know the definition of non-repudiation, rather it seems National Institute of Standards and Technology (NIST) isn't even consistent in the definition, and as a result this hurts workshops like the one I participated in. When Subject Matter Experts (SMEs) are looking for official definitions, we will generally look to the NIST Glossary. Interestingly, if we look up the definition of non-repudiation we find the following:

> Assurance that the sender of information is provided with proof of delivery and the recipient is provided with proof of the sender’s identity, so neither can later deny having processed the information.

This definition comes to us from NIST SP 800-18 rev. 1, and is also used two volumes of NIST SP 800-60. So, straight forward, right? Not really. This definition is adapted from another source document, CNSSI 4009 (warning: it's US DoD website using a DoD CA your browser may not trust). Okay, so what does the Department of Defense say about the definition of non-repudiation? It should be the same as above, right?

> Protection against an individual falsely denying having performed a particular action. Provides the capability to determine whether a given individual took a particular action such as creating information, sending a message, approving information, and receiving a message

Right, so we already have a pretty significant divergence. The first definition is stating that the "sender is provided with proof of delivery" and the "recipient is provided with proof of sender's identity." Whereas the second definition is stating the actual, correct definition - "Protection against an individual falsely denying having performed a particular action." Oddly enough, CNSSI 4009's definition comes from NIST SP 800-53 rev. 4 so why did NIST adapt the definition from CNSSI 4009? I don't think we'll know that answer, but it questions something...if NIST adapted the words from CNSS, did CNSS adapt the definition from NIST? Nope! The words are the same. In fact, at the time of this writing, rev. 4 was withdrawn and replaced with SP 800-53 rev. 5 which has nearly the exact same definition as in rev 4.

Okay, so what is the right answer and where did all this start? Well SP 800-53 doesn't give us any clues that they adapted it from anywhere else, but interestingly, there is a really concise definition in NIST's glossary. In fact, it's the definition I'm most familiar with, and it comes from none other than the February 1992 publication of the Foundations of a Security Policy for Use of the National Research and Educational Network (NISTIR 4734) which states:

> The inability to deny responsibility for performing a specific act.

Why could NIST's own definitions be so ... all over the place? Your guess is as good as mine, but since NIST is a standards setting organization, it would be ideal if they didn't have such different definitions. So, what is the problem with an adapted definition? Primarily, the issue starts when we have conversations in workshops where time is limited and someone is trying to get a point across. The first definition in the glossary isn't the one I would want readily available when trying to deal with the nuances of the core security concepts. I would actually say that the first one listed (which comes from NIST SP 800-18) isn't entirely correct. Let's break it down:

The first part is correct, but everything goes south when we hit "the recipient is provided with proof of the sender's identity". This is authentication, not non-repudiation. Just because you have received proof of the sender's identity, doesn't mean that the sender in fact sent the message. Identity is established through authentication, and authentication has not been connected to the message through something that provides both integrity and non-repudiation assurances. By adding that second part on proof of the sender's identity has now made the definition circular. Now, I don't believe that NIST meant for this interpretation. I actually believe that they were trying to adapt the definition to better clarify points made in SP 800-18, as glossaries in guidance documents tend to do. As someone that has written standards for an employer, I get the need to do this, but we must be careful that the definition doesn't over apply the knowledge to your own clarification.

### So Which Definition to Use?

I would argue it makes sense to stick with the definition as stated in NISTIR 4734 - it's the simplest, cleanest, and most direct.

While Information Security has been around for some time, these concepts need to be left unadulterated for newer security domains, like Product Security. The top definition in the NIST glossary will cause confusion for new organizations that don't fit the conventional information technology domain. As an example, I previously worked for a silicon hardware vendor where I needed to work in a wide-range of hardware disciplines training teams to perform threat modeling with STRIDE, it's already difficult enough to make it clear how we may approach implementing that in hardware.

And I want to go back and address the workshop; do I think that the definition was going to cause problems, even though we used the "wrong" definition? No, not in the slightest. While there were differences I had with others in the committee, at the end of the day, the definition was being used to help clarify a point being made, and it wouldn't ultimately impact the created work products. It was the contention between myself and other SMEs that left me puzzled, and I wanted to better understand where I was wrong.
