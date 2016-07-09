---
layout: post
title: We've Lost Sight of the Basics
---

<rant>
I'm a penetration tester and I have a checklist that I use on just about every test I do. My checklist includes things like:

* Scan the external network for open SMB ports.
* Scan the internal network for shared folders with no authentication.
* Scan web servers for files like info.php, .htaccess, config.php, etc.
* Test every login for default credentials.

Do you know why these items are on my checklist? It's because they work. Inevitably some sysadmin or web admin has misconfigured their firewall, screwed up the file permissions on their server, or installed a system and didn't bother changing the default password (or worse yet, the vendor wouldn't let them.)

The reason we are losing the war in infosec is because we've lost sight of the basics. We don't segment our networks, we don't modify default passwords, we don't harden servers before putting them in production. Some of these tasks can be automated, some cannot but the initial investment of time is more than worth the long term benefit.

Many of the common vulnerabilities I find can be found with free or cheap tools in a matter of minutes. Often they can be fixed in a matter of days, if the desire to fix them is there.

It's been at least five years since I had to defend a network so maybe I'm out of touch but unless we find a way to fix these dumb mistakes and prevent them from happening again, we will never win the infosec war.

Here's a presentation I did recently to help illustrate the point [You Will Get Owned in 2016](https://github.com/averagesecurityguy/presentations/blob/master/will_get_owned_2016.pdf)

</rant>