---
layout: post
title: Cracking MongoDB Passwords
---

On a recent penetration test I came across a number of MongoDB servers that allowed unauthenticated access. Using this access, I was able to download the MongoDB user accounts and their associated password hashes. MongoDB uses two password hashing schemes. The first is called MONGODB-CR, which is a simple MD5 hash of the string username:mongo:password. This password hashing algorithm is no longer used and has been replaced by a much stronger password hashing algorithm based on SCRAM-SHA-1. When MongoDB introduced the SCRAM-SHA-1 algorithm they didn't update the older user accounts to use the new hashing algorithm so you will still find servers that use the older MONGODB-CR format.

I wrote two scripts to crack these passwords. The first, [mongodb_cr_crack.py](https://github.com/averagesecurityguy/scripts/blob/master/mongodb_cr_crack.py), is a Python script for cracking MONGODB-CR passwords that is multithreaded and can process a large number of passwords quickly because MD5 password hashes are easily calculated. This script uses Python3 and the standard libraries. To use this script run `./mongodb_cr_crack.py hashfile wordfile`, where hashfile is file containing a list of colon (:) separated usernames and password hashes (one per line) and wordfile is a list of password candidates.

The second script, [mongoscram.go](https://github.com/averagesecurityguy/scripts/blob/master/mongoscram.go), is written in Go, which worked much faster than Python for calculating the SCRAM-SHA-1 passwords. Since the SCRAM algorithm uses PBKDF2 with 10,000 iterations, cracking these passwords is compute intensive and takes a lot of time. The mongoscram.go script can test over 300 passwords per second for one user. To use the script you will need to install the latest version of the [Go language](https://golang.org) and you will need to install the PBKDF2 library using `go get http://golang.org/x/crypto/pbkdf2`. You will also need to define the environment variable GOPATH (On Linux or Mac add `export GOPATH=$HOME/go` to your .bash_profile file.).

When running the mongoscram.go script you will need to provide the username, password_file, salt, and stored_key. The username, salt, and stored_key can be obtained from the MongoDB server. The password_file is the list of passwords you want to test.

As always, if you have any trouble running the scripts or getting them to work please let me know and I will be happy to help.