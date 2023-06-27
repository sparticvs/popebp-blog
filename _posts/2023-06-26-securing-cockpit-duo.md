---
title: Securing Cockpit + Duo
date: Jun 26, 2023
author: sparticvs
tags:
  - system-administration
---

A few years ago I did a nice write-up on Cockpit + Duo Security 2FA. Since then, CentOS Stream 8 updates pulled in functionality from Cockpit upstream that introduces some challenges. One of these features displays "Other Options" on the login menu with a "Connect to" prompt. The issue with this is that it allows an exposed Cockpit instance to act as a proxy which bypasses the 2FA check. I was very worried about this and [opened an issue with the project](https://github.com/cockpit-project/cockpit/issues/17340). Lo and behold, a solution already existed.

## Hardening Cockpit Further

