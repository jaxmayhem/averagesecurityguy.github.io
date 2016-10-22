---
layout: post
title: Recon-ng + Google Dorks + Burp = ...
---
The other day I asked on Twitter, what tools Blue Teams or Red Teams wished they had. I'll admit, it was selfish on my part because I really want to be able to build and sell a usable product. Anyway, @ethicalhack3r said he wanted a way to search for Google Dorks and get them into Burp to find interesting content. So I decided I'd take up the challenge.

Sometimes, I like to reinvent the wheel because I feel like I can make a better wheel but I knew Recon-ng already had Google Dork searches built in and had a method for dealing with Google's CAPTCHAs. And, as much as I'd like to think I could make a better wheel than Recon-ng, I know I can't. So I figured the next best thing would be to build a report module that could take the URLs found using Google Dorks and send them to Burp, so that's exactly what I did.

When the recon/domains-vulnerabilities/ghdb module is run it uses a large number of Google Dorks from the Google Hacking Database to search a site for interesting content. When it finds matching URLs they are placed in the vulnerbilities database with the category 'Google Dorks'. Recon-ng can run direct queries on the database so I was able to search for all of the URLs where the category matched 'Google Dorks'. Once that was done, I used the request method to get each URL. The trick to getting these URLs into Burp is to set the global PROXY value before running the report and then unset it after running the report.

To use the new reporting module:

1. Run the recon/domains-vulnerabilities/ghdb module and gather the dorks you want.
2. Set the global proxy:

    a. Use the `back` command to leave the module context and enter the global context.
    b. Use the `set PROXY http://<your_proxy_here>` command to set the global proxy

3. Enter the proxifier reporting module using the command `use reporting/proxifier`.
4. By default the module will find the vulnerability URLs with a category of 'Google Dorks' but any query that yields a list of URLs can be used.
5. Run the module with the `run` command.
6. Unset the global proxy:

    a. Use the `back` command to leave the reporting module.
    b. Use the `unset PROXY` command to unset the global proxy.

Thanks to @ethicalhack3r for the idea and to @LaNMast3r for recon-ng and help writing the module.


