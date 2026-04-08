---
title: Reported Vulnerabilities
icon: fas fa-bug
order: 5
---

I have reported the following vulnerabilities.

### Vulnerability in CSRF-Magic

**Summary**

CSRF-Magic, a PHP library, is used to provide Cross-Site Request Forgery protection. During a configuration inspection of pfSense firewall, it was identified that when `$GLOBALS['csrf']['secret']` was left uninitialized, the CSRF Token was predictable.

While reviewing the source code for CSRF-Magic, there was a comment that specifically called out using `csrf_get_secret()` instead of directly accessing the global value. The reason for this was that the accessor function would generate a random session for the server instance when the global configuration did not provide a secret.

**Details**

- **Assigned CVE:** [CVE-2013-7464](https://nvd.nist.gov/vuln/detail/CVE-2013-7464)
- **Date Reported:** 23/5/2013
- **Date Remediated:** 17/7/2013
- **Acknowledgement:** [Github Commit](http://repo.or.cz/csrf-magic.git/commit/9d2537f70d58b16aeba89779aaf1573b8d618e11)
