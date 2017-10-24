---
layout: post
title:  "Security and Cryptography"
date:   2017-10-24 08:08:26 +0100
categories: tools
---
Encrypt tar.gz file on create

Pack your_dir in a encrypted archive your_archive.tgz.gpg (symmetric encryption):

tar -cz your_dir | gpg -c -o your_archive.tgz.gpg

Unpack it:

gpg -d your_archive.tgz.gpg | tar xz

Check keys
Ubuntu: Start menu: Password and keys


Folder enc
https://www.maketecheasier.com/create-encrypted-directory-in-ubuntu/


    The biggest dangers come from the possibility of political change — we’re putting in powers and infrastructure that could easily be badly misused by a future government… These powers are actually better suited for monitoring and controlling political dissent than catching criminals and terrorists — they’re ideal for an authoritarian clampdown should a government wish to do that. A future government might well.

Suddenly, the world of George Orwell’s 1984 is closer than ever.
http://www.makeuseof.com/tag/technology-explained-how-the-internet-works/

https://www.youtube.com/channel/UCFj8QXb5Dtqs8ZmEjCBUchg

# Security

# Router security

# File Security

gpg

The passprase is the Achile's heel, easy to crack using dictionary based attacks. Protect your's ~/.gnupg folder.

Don't use telenet. Disable telenet service from router.

# OS
Whonix is a Tor based Linux distribution
https://www.whonix.org/
tails


# Wi-fi Leakings

Don’t Forget to Turn Off Your Wi-Fi. Wi-fi spots do spy on you. Moreover they can be turned into stingrays.

 A larger initiative called Smart Places, which is a global project for rolling out this real world cookie.
 Opt-out
Use opt-out: https://optout.smart-places.org/

When you turn Wi-Fi on for your device, it will search for a AP to connect to in “active scanning” mode. In order to do that it will show your MAC address to nearby APs. This is a physical address associated with your specific device. Once connected to the hotspot you are granted an IP address that will allow you to connect to the internet. So there are two identification methods; your MAC address between you and the AP, and your IP address between you and the internet.

http://www.makeuseof.com/tag/9-awesome-ways-use-nfc-thatll-impress-friends/
http://www.makeuseof.com/tag/wi-fi-can-track-around-world/

# Do not track
Did you know that companies could just ignore Do Not Track? Do you use other anti-tracking features to ensure your privacy? Use Disconnect.me
http://www.makeuseof.com/tag/not-track-actually-work/


# Surveillance Avoiding

Don’t Forget to Turn Off Your Wi-Fi

http://www.makeuseof.com/tag/avoiding-internet-surveillance-complete-guide/
http://www.makeuseof.com/tag/wi-fi-can-track-around-world/
A Stingray is a “fake cell tower” that can intercept cellphone communication. They then link this to you by using your SIM card’s International Mobile Subscriber Number (IMSI). This was only possible using cellular network connections and not Wi-Fi.

# Password strength

Keep it safe.

_Amateurs hack systems, professionals hack people. — ‘’’Bruce Schneier’’’__ 



Pick a pattern on your keyboard and type it with alternating use of the SHIFT key, e.g. Xdr%6tfCvgz/

http://www.makeuseof.com/tag/7-ways-to-make-up-passwords-that-are-both-secure-memorable/
http://www.makeuseof.com/tag/create-strong-password-forget/


# DNS Leaking
www.dnsleaktest.com.

# VPN
http://www.makeuseof.com/tag/virtual-private-network-work-technology-explained/

http://www.makeuseof.com/tag/dns-leaks-can-destroy-anonymity-using-vpn-stop/


For folder encryption you need: ecryptfs, vezi: https://help.ubuntu.com/lts/serverguide/ecryptfs.html

A keyring is a secured "stored database" of your login information stored a removable media. It's wrapped by encryption schema (PKCS#11).


jazio@798kiyt ~/Documents/journaling $ ecryptfs-manager

eCryptfs key management menu
-------------------------------
	1. Add passphrase key to keyring
	2. Add public key to keyring
	3. Generate new public/private keypair
	4. Exit

Make selection: 1

	Mount-wide passphrase: 
	Confirm passphrase: 
	Using the default salt value

Added key to keyring with signature [711467d43760472f].

