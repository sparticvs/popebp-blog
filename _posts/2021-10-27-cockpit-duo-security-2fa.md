---
title: Cockpit + Duo Security 2FA
date: Oct 27, 2021
author: sparticvs
tags:
  - system-administration
---
![Cockpit-Duo](https://github.com/sparticvs/popebp-blog/assets/847020/3b9e430d-971e-4dba-ba9f-bdd5524adbb5)
## Background
For regular visitors you may have noticed that over the past couple weeks, things have been offline. I left my previous job and with that change, there has been some additional changes that I made. I recalled the server from the datacenter and set it up locally to act more as a lab host. After some inspection, I found a drive was failing so I swapped it out and restored the OpenZFS RAID-Z2. After resilvering completed, I rebooted the machine to update to the latest kernel, and that is when everything went south.

I found I wasn't able to boot anymore and the reason was that dracut didn't package in the ZFS modules and binaries that were needed for boot. I could fix it, but I decided against it. Why? The system was a full CentOS major release behind. I wanted to get on CentOS Stream anyway. So, after rebuilding it, I decided to use [Cockpit](https://cockpit-project.org/) to help with managing. Again, I want this to primarily act as a lab machine, so being able to quickly spin up VMs, get to a VNC and interact and then destroy the VM is important to me.

Part of the value of having the lab machine is to give me the ability to give presentations on campus here about security ops in a linux environment. I want to get to Cockpit remotely, but I also don't want to deal with someone brute-forcing the login and ultimately getting root access on the host. I want Two Factor Authentication (2FA) to work, but Cockpit doesn't have a plugin to enable this on a case-by-case basis. Instead, Cockpit's session management uses the local Pluggable Authentication Modules (PAM) to authenticate users to Cockpit. This means I need a PAM-based 2FA setup.

In my research, I stumbled across a similar discussion on the [NethServer Community forums](https://community.nethserver.org/t/2fa-or-two-factor-authentication-with-cockpit/14172/3), although they were using Google Authenticator OTP (and later FreeOTP). This is was a great starting point, but I use Duo Security, and I want that up and running instead. That is what this blog focuses on.

## The Setup
Assuming you don't have Cockpit up and running, you will need to start that:
```
# systemctl enable --now cockpit.socket
```
With Cockpit running, you can access the console with `https://<your-ip\\>:9090/`. This is great, and you can login with a local user account. The downside is that I want 2FA to be required for all user logins. This will give me an audit trail and early notification if a password has been compromised.

I will also be using Duo Security's UNIX PAM, installed using the [Duo Unix Installation Guide](https://duo.com/docs/duounix#install-from-linux-packages). Quick note for folks, at the time of this writing Duo has a free tier that gives you the ability to support up to 10 users. After the repository is installed, GPG keys are added, and the `duo_unix` package is installed, we are ready to start configuring.

## Configuring Duo
Before getting to far, we want to configure Duo. You will need to log into your Duo Security account, add a new application (look for UNIX in the list). Once that is created you will be given some details needed in the next steps.

Open `/etc/duo/pam_duo.conf` in your favorite editor (note: this will need to be done as root). And set the `ikey`, `skey`, and `host` fields to match with what the Duo webinterface is telling you. Then you will want to add the following to the bottom of the file:
```
pushinfo = yes
autopush = yes
```
`pushinfo` will tell Duo's service what command is being run. This is useful for auditing later on to see what happened. It can also push that information to your phone.

`autopush` tells Duo to not ask the user for an option and automatically perform a Duo Authenication Push notification to the registered device.

Cockpit will work without `autopush = yes` (the default is no) and the Web UI will prompt you for which option. It won't look pretty and will be hard to read quickly, but it will work. I opted for autopush because it saves me a step.

## Configuring PAM
Now, we need to configure PAM. Open `/etc/pam.d/cockpit` in your favorite editor (note: this will require root permissions to edit) and add the following line just after `auth substack password-auth`:
```
auth required pam_duo.so
```
Your Cockpit PAM session should now read:
```
#%PAM-1.0
auth       required     pam_sepermit.so
auth       substack     password-auth
auth       required     pam_duo.so # !! Add the line here !!
auth       include      postlogin
auth       optional     pam_ssh_add.so
account    required     pam_nologin.so
account    include      password-auth
password   include      password-auth
# pam_selinux.so close should be the first session rule
session    required     pam_selinux.so close
session    required     pam_loginuid.so
# pam_selinux.so open should only be followed by sessions to be executed in the user context
session    required     pam_selinux.so open env_params
session    optional     pam_keyinit.so force revoke
session    optional     pam_ssh_add.so
session    include      password-auth
session    include      postlogin
```
After saving the file, we need to restart Cockpit, so that cockpit-session can reload it.
```
# systemctl restart cockpit
```
## Fixing SELinux
If you are on an Enterprise Linux distribution like myself (so CentOS) you will find that you can log into Cockpit still, but the Duo Push never happened. This is because there are SELinux policy failures. As part of the pam_duo.so, it is making a TLS connection to the "host" mentioned in the Duo configuration file. Since the cockpit-session binary is loading this library, it is making the call, which is not expected behavior. We need to adjust the SELinux policy.

If you have logged into Cockpit, and enabled administrative access, you can see the failure in the SELinux menu. There are a number of guesses that the tools make to try to figure out what is happening, but luckily for you I already did the leg work. As mentioned before, it's because of the TLS connection outbound that isn't expected. To fix this issue, we can do the following:
```
ausearch -c "cockpit-session" --raw | audit2allow -M cockpit-session-duo
semodule -X 300 -i cockpit-session-duo.pp
```
So what is that command doing? `ausearch` searches the audit logs for the cockpit-session command and outputs the failure in raw, script-readable format. Next we pipe that into `audit2allow` which will convert the failure information into a policy file that will be named `cockpit-session-duo.pp` (the .pp is added by audit2allow and actually there is a second file that is created, so don't add the .pp).

The next command is to install the new policy with a priority of 300. This is recommended by the SELinux notes in Cockpit.

And that's it. If you are currently logged into Cockpit, log out, wait a couple seconds and login. I found that the first attempt fails, but every attempt after will work, and you will receive a push notification before the login completes (assuming you used `autopush`).
