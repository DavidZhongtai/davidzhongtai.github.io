---
title: "Bugs"
---

## Bug Reports

Got bored so here is a running of list of reports and finds in my spare time. All were found accidentally and reported to their respective security groups immediately.
| Organization | Find | Date |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- |
| **Cloudera** | In progress, reported on 1-28. The fix and patch is still in progress.  | 1-28 |
| **AllenAI** | An exposed `localhost` port allows an actor to access production builds as an elevated user. No user authentication deployment and configuration of builds as a non-admin user. Unauthorized builds allow for credential dumping by printing to console; additionally, Firebase and GCloud credentials were exposed. Reported and fixed within 12 hours of report. | 1-25 |
| **Catalogic** | An exposed server port allows an actor to access Jenkins build pipelines and internal developer lists without authentication. In addition to that, an actor is given elevated privilege to delete and create workspaces as well as view build log data which included environment variables. Giving unauthorized build access allows for a user to dump credentials without administrative access detailed in [this article](https://www.codurance.com/publications/2019/05/30/accessing-and-dumping-jenkins-credentials)| 1-23 |
| **[Redacted]** | Discovered backdoor to allow for access to the whole codebase and pipelines. Build access was disabled, but credentials remained unencrypted and unsecured in credential store. Both iOS and Android development and production builds were exposed. Reported and fixed within 24 hours of report (on a Sunday). The detailed writeup can be found [here](/posts/pwn) | 1-21 |
