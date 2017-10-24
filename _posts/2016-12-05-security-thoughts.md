---
layout: post
title:  "Security thoughts"
date:   2017-10-24 08:08:26 +0100
categories: frameworks
---

Defend against keyloggers
linux key loggers needs to have a root access before they can monitor the keyboard.
In order for a keylogger to function, it would require an active process. Take a snapshot of your processes when the system is initially installed/clean and then from time to time run a process listing check. If new processes appear, then you will be able to quickly detect and eliminate any undesired one. If you require to run new ones, just update the valid process list.
This can be made a little easier: a script to output the process list to a file, or you can even take it a little further and schedule-run a script to compare the running processes with the initial ones you know to be valid.
The only thing that you can do is check for rootkits. To do that you can use CHKROOTKIT (a powerful tool to scan your linux for trojans)

Then, if a keylogger is running, it's process(es) will be visible. All you need to do is use ps -aux, or htop to look at the list of all running processes and figure out if anything is suspicious.

    The most common "legitimate" Linux keyloggers are lkl, uberkey, THC-vlogger, PyKeylogger, logkeys. logkeys is the only one available in the Ubuntu repositories.
Usually this risk is very minimal on Ubuntu/Linux because of the privileges (su) required.

http://askubuntu.com/questions/169887/how-can-i-detect-a-keylogger-on-my-system

You can use your own wireless keyboard.


Apache removeip

This module is used to treat the useragent which initiated the request as the originating useragent as identified by httpd for the purposes of authorization and logging, 
even where that useragent is behind a load balancer, front end server, or proxy server.
The module overrides the client IP address for the connection with the useragent IP address reported in the request header configured with the RemoteIPHeader directive.



Reverted euaid_collaborative.field_instance.                                                                                                                                          [ok]
WD features: Attempt to update field field_euaid_lea_activities failed: Cannot change an existing field's type. 

torrenting: Disable DHT, use peerblocker (spy peers).

Google 

Disable Search Customization:  Signed-out search activity = off
Ads Settings: Google Search Ads based on your interests = off
Youtube Customization: Videos you watch on YouTube = off / Videos you search for on YouTube = off
Google Analytics Opt-out Browser Add-on. (still on doubt since is Google)


Port Forwarding

A firewall protects a computer by blocking unauthorized information, but if a firewall blocked all the incoming and outgoing data, the computer would be unable to access the Internet. When a computer user wants some data to go through the firewall and to send it to a specific location, he can set up port forwarding. This gives the firewall instructions about which types of data are allowed and how they should be directed.


# Create a self signing certificate.



sudo yum install openssh
openssl version
# Step 1. generate the private key.
openssl genrsa 1024 > jazio-ssl-self-signed-certificate.key
openssl req -new -key ./jazio-ssl-self-signed-certificate.key > jazio-ssl-ssc-certificate.csr
# Generate the x509 certificate valable for 1 year
openssl x509 -in jazio-ssl-ssc-certificate.csr -out jazio-ssl-ssc-certificate.crt -req -signkey jazio-ssl-self-signed-certificate.key  -days 365