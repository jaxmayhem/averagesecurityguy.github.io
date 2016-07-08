---
layout: post
title: DNS Footprinting
---

There are a lot of tools available for doing target footprinting, Spiderfoot, Maltego, and theHarvester to name a few. Unfortunately, I find something lacking in each of these tools. Spiderfoot and Maltego are too complicated for me. I really like the Unix philosophy of simple tools that do one thing well and both of these fall outside of that philosophy. TheHarvester fits much better into this philosophy but it also provides a lot of data I don't want when doing network footprinting, like email addresses and shared hosts.

When I am trying to footprint a network I am often only given a domain name and I want to know DNS names and IP addresses associated with that domain name. In addition, I want to know about the network blocks those IP addresses belong to and other servers that may be in those network blocks. With that in mind I wrote the [resolve.py](https://github.com/averagesecurityguy/scripts/blob/master/resolve.py) Python script.

## Overview
The resolve.py script takes a domain name and provides the SOA record, MX records, and NS records. It then attempts a zone transfer from each of the name servers and then brute forces DNS names using the provided word list. Next, it does a whois lookup to find Network blocks associated with any IP addresses found in the A and AAAA records. Finally, it performs a reverse lookup on all of the identified IP addresses and on the small network blocks.

## Dependencies
The following Python3 libraries are needed.
* dnspython3
* netaddr
* ipwhois

## Usage
`resolve.py domain wordlist`

You can find an example of the output here: [http://pastebin.com/yUxjeTcj](http://pastebin.com/yUxjeTcj)


## Update 2016-01-20:
There is now a multi-threaded version of the script, [resolve_mt.py](https://github.com/averagesecurityguy/scripts/blob/master/resolve_mt.py). The usage is the same as resolve.py.