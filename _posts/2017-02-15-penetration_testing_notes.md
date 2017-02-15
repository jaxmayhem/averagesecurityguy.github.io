---
layout: post
title: PTNotes: A Simple Pentest Note Taking Tool
---

During penetration tests I often find myself making notes about hosts or about the engagement itself in a single text file called notes. Throughout the engagement, I refer to this file to see where I stand on the engagement. Some notes are about a compromised host such as how it was compromised and what data was gathered from it. Some notes are about general attacks such as SSH bruteforcing or directory busting and the successes and failures associated with those attacks.

In the past, I wrote a tool called Low Hanging Fruit, which parsed a Nessus file and pulled out the most obvious attack routes. I decided to take this idea and merge it with my note taking process into a simple tool that allows me to see both potential attack routes and take notes about the attacks and hosts. There are other tools that provide similar functionality but I've always found them to be too complicated.

To use [PTNotes](https://github.com/averagesecurityguy/ptnotes), start by creating a new project and importing Nmap or Nessus data. Each time you import data, the data is analyzed for additional attack vectors.

https://averagesecurityguy.github.io/assets/ptnotes_projects.jpg

Once you have imported data, you can view the project to see potential attack vectors and a summary of hosts and open ports. From the summary page you can view click on a host and see all of the imported Nessus and Nmap data for that host.

https://averagesecurityguy.github.io/assets/ptnotes_summary.jpg

You can view an attack and see a list of hosts that may be vulnerable to that attack. You can also add any notes to the attack to document the hosts you have tested and what successes or failures you had.

https://averagesecurityguy.github.io/assets/ptnotes_attack.jpg

From the attack page, if you click on a host you can see the Nessus or Nmap output that caused the host to be flagged for the attack. If the host does not have a link then the attack was flagged because of its port and protocol.

If you are searching for an easy way to take notes during your next Pentest engagement please give PTnotes a try. Also, if you have particular suggestions for improvements, please open an [issue on Github](https://github.com/averagesecurityguy/ptnotes/issues).
