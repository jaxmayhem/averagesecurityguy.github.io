---
layout: post
title: Sometimes You Need A Lot of Proxies
---
After building and testing my [Facebook Phone Enumeration](https://averagesecurityguy.github.io/2016/09/07/facebook-private-phone-enumeration/) script, I realized that if I want to run the script at scale I'm going to need a lot of proxy servers so that Facebook doesn't kill my enumeration. So I modified my [do_ssh_proxy.py](https://github.com/averagesecurityguy/scripts/blob/master/do_ssh_proxy.py) script to build out a number of proxy servers, create the appropriate SSH connections for a SOCKS proxy, and then build a proxychains.conf file. I've tested the script on Kali Linux running as root. If you decide to run it on a different setup let me know how it goes. You can find the script [here](https://github.com/averagesecurityguy/scripts/blob/master/do_proxy_chains.py).

To setup your proxies run the script with the create command:

    do_proxy_chains.py create 10 ids.txt

This will create 10 droplets and store the droplet ids in the ids.txt file so they can be cleaned up later. Be patient because creating droplets takes time. After creating the 10 droplets, it will create an SSH -D connection to each server. Once all of the SSH connections are created, the /etc/proxychains.conf file is written to use one random proxy server per request.

Once you are finished with the proxy servers you can destroy all of the droplets using the script:

    do_proxy_chains.py delete ids.txt

This will read each droplet id stored in the file and destroy the droplet. This will also delete the /etc/proxychains.conf file. To clean up the SSH connections you can use the following bash one-liner:

    ps -ef | grep [S]trictHostKeyChecking | awk '{ print $2 }' | xargs kill
