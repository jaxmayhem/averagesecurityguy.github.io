---
layout: post
title: DNS Footprinting at Scale
---

Recently I wrote an article on doing domain footprinting. Shortly after that article a friend on Twitter mentioned that he was doing zone transfer research against the Alexa top 1 million web sites so I decided to try my hand at it as well. My work on that project eventually resulted in code, raw data, and some analysis, which can be found here: 
[https://github.com/averagesecurityguy/axfr](https://github.com/averagesecurityguy/axfr).
 

Part of the analysis from the zone transfer research resulted in a huge list of subdomain names. I took the top 10,000 subdomains and used a modified version of the [resolve_mt.py](https://github.com/averagesecurityguy/scripts/blob/master/resolve_mt.py) script to foot print the Alexa top 1000 domains.

The modified script, [dnsbrute.py](https://github.com/averagesecurityguy/scripts/blob/master/dnsbrute.py), that I used and the resulting [dataset]({{ site.baseurl}}assets/footprint_data.tar.gz) in tar.gz format are both available. The dnsbrute.py script only works on one domain at a time so I used the GNU parallel program to run 8 copies of the script in parallel. I can get through the top 1000 domains within a day. Most domains take anywhere from 2 -10 minutes depending on how fast their DNS servers respond.

To run the script in parallel use the following command:

    parallel -a domain.list -j 8 ./dnsbrute {1} subdomain.list

Make sure you have Python3 installed and that the dnspython3, netaddr, and ipwhois libraries are installed.