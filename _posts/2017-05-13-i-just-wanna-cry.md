---
layout: post
title: I Just WannaCry
---
So apparently there was a ransomware worm this the weekend. If it hadn't been for my entire Twitter feed blowing up about it, I probably wouldn't have known. :) The more I read my feed though the more frustrated I get so I decided to write down my thoughts.

* First, mad respect to all the folks who worked tirelessly to analyze and reverse engineer this worm. I have to say, there was nothing accidental about @MalwareTechBlog saving the day. Even if they didn't know the exact purpose of the domain, the fact that they found it in the code and registered it shows they were busting their butt to understand the worm and that's not accidental.

* Second, there appears to be a lot of controversy concerning who's to blame. One group says the orgs who didn't patch are to blame, another group says the NSA is to blame, and still another group says the malware author is to blame. The funny thing is they are all right. The NSA could have disclosed the vulnerability sooner but it doesn't matter because the vuln was disclosed and patched months ago. The malware authors didn't have to write the code and release it but again it doesn't matter. This is not the first time a large scale worm has disrupted the world. Anyone remember I Love You, Sasser, Conficker? Finally, orgs didn't have to leave their unpatched/unpatchable machines on the network but guess what, they do and they will.

* Third, based on my Twitter feed there is only one solution to the problem, patching, and there are many orgs that just can't do that for whatever reason. For a bunch of hackers, we sure are bad at thinking outside the box. First, you can turn off SMBv1, second you can enable the Windows firewall. If for some reason you can't do either of those things because you are afraid to touch the software, you can segment the device using a hardware firewall or with a layer 3 switch, both of which are readily available. Finally, you can push the vendor for updates.

I was a sysadmin once, I know it's tough to get everything patched and I know vendors can be painful to deal with but I also know we can all do more to protect our networks and our customers/clients/users.
