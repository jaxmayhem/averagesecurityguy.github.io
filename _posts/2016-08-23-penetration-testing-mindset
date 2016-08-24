---
layout: post
title: The Penetration Testing Mindset
---

Many penetration testers want to send an exploit to pop a box and call it a day, but a single
exploit is rarely enough to achieve the goals of a penetration test. Most penetration testing goals
require exploiting multiple weaknesses throughout a system. As an example, a tester may need
to compromise an internal user’s machine and then pivot through it to get to an internal
database. Testers with the one-and-done mindset will find themselves often frustrated and failing
to accomplish the goals of the penetration test. Instead, a good tester will continually assess the
goals of the test, their current information or access level, the information or access level they still
need, and the ways in which they can obtain what is needed from their current vantage point. An example of
the continual assessment mindset is given below.

    Gail needs to access the sensitive data stored in a Microsoft SQL server. To access the
    server she wants to get the username and password for a domain administrator account,
    an SQL admin account, or the sa account. Gail currently has network access to the
    server and other devices on the network. She attempts to brute force the sa account,
    which fails. Next, she scans the SQL server and other network devices for exploitable
    vulnerabilities. The SQL server does not have any exploitable vulnerabilities but another
    server on the network does. After compromising the other server, she now has access to
    the hashed password of the local administrator account. She then accesses the SQL
    server using the local administrator password but still cannot access the data in the SQL
    server. Fortunately, a SQL admin account was used to run a Windows service. Gail is able
    to use her administrative access to impersonate the SQL admin’s security token and is
    then able to access the data in the SQL server.

By continually assessing her situation, Gail was able to accomplish her goal even though she did
not achieve the goal in the intended manner.
