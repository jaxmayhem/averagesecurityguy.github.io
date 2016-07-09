---
layout: post
title: Web Content Discovery with Parallel
---

In my previous post I showed you how to do content discovery using a bash one-liner and the dirb program. This works great if you have 5-10 servers but if you have more than that you may need to run the bash command on multiple servers at the same time. This is where the parallel command can help.

If the parallel command is not installed on your Kali box, you can install it with `apt-get install parallel`.

Using the following command we can run dirb against 16 servers at once.

    cat websites.txt | parallel -j 16 dirb {} -f -o websites.dirb

All of the stdout from all 16 jobs will be written to the websites.dirb file. Once the command is completed you can grep the websites.dirb file for any identified files. The command `grep + websites.dirb` should produce results similar to the following:
 
    + https://yahoo.com/t (CODE:302|SIZE:257)
    + https://twitter.com/tos (CODE:200|SIZE:3751)
    + https://yahoo.com/ticket (CODE:200|SIZE:0)
    + https://yahoo.com/ticket_list (CODE:200|SIZE:0)
    + https://yahoo.com/ticket_new (CODE:200|SIZE:0)
    + https://yahoo.com/tickets (CODE:200|SIZE:0)
    + https://netflix.com/_borders (CODE:504|SIZE:0)
    + https://netflix.com/_database (CODE:504|SIZE:0)
    + https://netflix.com/_js (CODE:504|SIZE:0)
    + https://netflix.com/~apache (CODE:504|SIZE:0)
    + https://netflix.com/apis (CODE:301|SIZE:0)
    + https://netflix.com/crossdomain.xml (CODE:200|SIZE:3)
    + https://craigslist.org/about (CODE:302|SIZE:1)
