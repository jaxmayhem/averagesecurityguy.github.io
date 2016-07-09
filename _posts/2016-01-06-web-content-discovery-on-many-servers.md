---
layout: post
title: Web Content Discovery on Many Servers
---

Often on black box network tests I run across a large number of web servers on the network. I like to look for common files on all of the web servers I identify because you never know when you may run across a configuration file, a php info file, or some other interesting bit of information. When there are 10s of servers to check I don't have time to kick off each scan and babysit it until it is done so I use a simple bash one-liner to help me out.

This one-liner assumes you have a text file with each of your web servers listed on a separate line in the following format: `http(s)://servername_or_ip:<port>`. It also assumes you have the `dirb` program installed, which should be installed in Kali or can be installed with `apt-get install dirb`.

Here is the one-liner:

    for u in $(cat web_servers.txt); do dirb $u -f; done

If you would like to use a different word list add the path to the word list after the $u like this:

    for u in $(cat web_servers.txt); do dirb $u /path/to/wordlist -f; done
