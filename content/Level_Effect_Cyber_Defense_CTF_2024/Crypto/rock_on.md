---
title: "Rock On"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Cryptography','Medium','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Crypto](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/bits_abound)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

### Getting it out is the easy part, but good luck getting in.

Here we are given a capture.pcap to download and inspect.
Opening the pcap with wireshark we can quickly see some http traffic, as well as a GET request for a flag.zip.
 
![rock_on_1](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/rock_on_1.png?raw=true)

Next, we can export the file to proceed to the next step.
Trying to unzip the file reveals that it is password protected. We will need to guess the password in order to continue. We can do this using the Rockyou wordlist and JohnTheRipper.

> zip2john flag.zip > zip_hash.txt

>john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

>john --show zip_hash.txt


![rock_on_2](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/rock_on_2.png?raw=true)

Unzipping this gives us a flag.pdf file which, surprise surprise, is also password protected. We can repeat the process for the pdf:

>pdf2john flag.pdf > pdf_hash.txt

>john --wordlist=/usr/share/wordlists/rockyou.txt pdf_hash.txt

![rock_on_3](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/rock_on_3.png?raw=true)


Finally, we can use the cracked password to open the PDF and get the flag:

![rock_on_4](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/rock_on_4.png?raw=true)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/bits_abound)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)