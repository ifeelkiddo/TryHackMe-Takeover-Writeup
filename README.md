**TryHackMe {TakeOver Walkthrough}**

This challenge revolves around subdomain enumeration.

Hi.. I am glad to see you here. In this article I will walk you through TakeOver room by Tryhackme.

**Context**
Hello there,
I am the CEO and one of the co-founders of futurevera.thm. In Futurevera, we believe that the future is in space. We do a lot of space research and write blogs about it. We used to help students with space questions, but we are rebuilding our support.
Recently blackhat hackers approached us saying they could takeover and are asking us for a big ransom. Please help us to find what they can takeover.
Our website is located at https://futurevera.thm

_Hint: Don't forget to add the MACHINE_IP in /etc/hosts for futurevera.thm_

**Question**

What's the value of the flag?
Answer format: ****{********************************}

**Solution**
**Step-1:** According to the hint provided we need to add the Ip address and domain in the "Hosts" file located in "etc" directory
**The /etc/hosts file is a system file used by operating systems (like Linux, macOS, and Windows) to map hostnames (domain names) to IP addresses.**

Step-2: Perform a simple nmap scan to know what services are running in our target machine.
nmap scan resultThere is a website running on port 80
futurevera.thm

Our first step will be identifying subdomains, for which we will use the ffuf tool.
ffuf -c -w /usr/share/wordlists/SecLists/Discovery/DNS/bitquark-subdomains-top100000.txt -H 'Host:FUZZ.futurevera.thm' -u https://10.10.60.14
FFUF
-w :Wordlist file path eg. '/path/to/wordlist:KEYWORD'
-c : Colorize output.
-H : Header `"Name: Value"`, separated by colon. Multiple -H flags are accepted.
-u Target URL

ffuf outputHere we can see that we are getting too many unwanted stuff
So, we will filter out unwanted subdomains by using "-fs 4605" in our command which will filter out all the subdomain with HTTP RESPONSE SIZE 4605
ffuf outputNow we will add support.futurevera.thm and blog.futurevera.thm in our hosts file 
There is some recreation work on going on support.futurevera.thm
support.futurevera.thmI checked the source code to look for something, but didn't find anything. Then, I examined the certificate and discovered something interesting i.e the DNS name.
DNS nameAdd the DNS name you found to the hosts file, just like we did for futurevera.thm . Then, open the DNS name in your browser, and you'll find the flag in the URL.
Congratulations! You found the flag. 🤩🎉🎉
Note: Always remember to review the "page source" and "certificates," even though they may not always contain useful information.

---

🧑‍💻Happy Hacking!!!
