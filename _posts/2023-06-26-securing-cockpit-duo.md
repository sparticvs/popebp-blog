---
title: Securing Cockpit + Duo
date: Jun 26, 2023
author: sparticvs
tags:
  - system-administration
---

A few years ago I did a nice write-up on [Cockpit + Duo Security 2FA](https://popebp.com/2021/10/27/cockpit-duo-security-2fa.html). Since then, CentOS Stream 8 updates pulled in functionality from Cockpit upstream that introduces some challenges. One of these features displays "Other Options" on the login menu with a "Connect to" prompt. The issue with this is that it allows an exposed Cockpit instance to act as a proxy which bypasses the 2FA check. I was very worried about this and [opened an issue with the project](https://github.com/cockpit-project/cockpit/issues/17340). Lo and behold, a solution already existed.

## Hardening Cockpit Further

First we need to edit the configuration for Cockpit which is at `/etc/cockpit/cockpit.conf`. My install didn't have a configuration file, so I had to create a new file there and add the following content:

```ini
[WebService]
LoginTo = false
```

Now the last action is to restart cockpit to load in the new configuration.
```
# systemctl restart cockpit.socket
```

And that's it!

## But There's a Catch

People should really be aware of the very real risk here to your system with exposed web-based admin panels...it's like exposing your IPMI interface to the internet...you should be aware of the risks before doing so. You could potentially be allowing an attacker to directly pivot into your network. Without the appropriate controls in place, there is more than just that host at risk.
