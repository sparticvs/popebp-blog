---
title: "Structuring Software Development Teams: A Response"
date: 2020-12-29 18:50:00 +0000
categories: [Security, Software Development]
tags: [security, software-development, team-structure, devsecops, psirt, privacy]
description: >-
  A response to the Steel Kiwi blog post about software development team structure, highlighting the critical missing pieces of security and privacy roles.
---

*These views are my own and do not reflect the opinion of my employer.*

Steel Kiwi, a bespoke Ukrainian software engineering firm, published (and subsequently shared on HackerNews) a post titled "Software Development Team Structure: Important Roles & Responsibilities". The blog post author included roles from DevOps to Business Analyst, but failed to include one of the most important roles - Security Engineer. In fact, there is absolutely no mention of Security anywhere in the blog post, which is terrifying given that the focus of the business is web and mobile application development.

I'm a security engineer, specifically, I manage the Product Security Assurance team at my employer - the team works closely with our engineering teams, ensure that product teams consider security threats, implement appropriate mitigations, and then our team performs assessments to identify flaws before (and after) the product goes out the door. We also serve as the single point-of-contact for external entities looking to report vulnerabilities in our products.

I'm disappointed that it seems Steel Kiwi has downgraded the importance of security within their teams. For companies that are working on structuring their software development teams for effectiveness, let me suggest some modifications -

### Security Training

Everyone on the team, and I mean everyone - you too BA - needs to receive Security training. What your training curriculum looks like will vary based on the role, but might I suggest looking at the Secure Software Practitioner (SSP) trainings from Security Compass for an introductory curriculum that fits the roles on the team. If your team primarily develops web applications, I recommend signing everyone up for OWASP Top 10 training (note: a Security Assurance Engineer on the team may be able to train everyone up on the Top 10).

### Security Assurance Engineer

Someone on the team needs to own the security in the product and they need to be enabled to veto a release if the security of the product may lead to a serious risk of compromise. This person will need to stay up-to-date on the latest in security attacks, develop and maintain the threat model for the product, and consult with the stakeholders around the risks associated with the threats and the cost-benefit tradeoffs for mitigations. This person should also be familiar with application security testing and the toolset of the hacker - ideally this person has some experience as a developer previously and can create new tools to exercise potential vulnerabilities before the product ships and hackers get to doing this. This person needs to be a subject matter expert - if you can afford to have multiple SMEs on the team that would be better - in cryptography, application security, and secure architecture. Ideally, this person is certified as an (ISC)2 CSSLP (Certified Secure Software Lifecycle Professional).

### (Dev)SecOps Engineer

It's great to have DevOps on your team, someone that can speak both the developers language and handle the operations side of the house, but it's not enough. Your team needs SecOps - when you launch your product to the world, hackers will go after it - DevOps doesn't have this skill on their own and many times will miss the signs of an attacker or won't have the knowledge about maintaining Web-Application Firewalls (WAFs), and Security Event and Incident Management tooling (SEIMs). If your product has a reduced attack surface, then covert your DevOps to DevSecOps with some training and support them with the budget to be able to monitor for attacks and be able to quickly apply compensating controls to protect your assets. The (Dev)SecOps engineer role is responsible for monitoring for attacks, and owning and managing security controls in the deployed environment. Ideally, this person would have a certification or previous experience in incident response. If you have a centralized Computer Security Incident Response Team (CSIRT) or a Security Operations Center (SOC), then the responsibilities of this role may belong with that team instead.

### Your Organization's PSIRT

The Product Security Incident Response Team (PSIRT) is a sister team to the CSIRT, and is growing in popularity across organizations. PSIRT's is responsible for receiving vulnerability reports and is generally a cross-functional team that includes individuals from various teams in the company. If your firm is small and doesn't have everyone that FIRST.org suggests to build a complete centralized team, consider splitting these roles up across your team and ensuring they have weekly meetings.

### Privacy

Finally, teams that develop web and mobile applications, also have to adhere to privacy laws around the world. Security and privacy go hand-in-hand, and it's possible to build a security team that also handles privacy, but this isn't the best idea depending on what sort of usage the customer will have with the collected data (and especially if Steel Kiwi remains the processor of said data, there may be legal obligations that require compliance).
