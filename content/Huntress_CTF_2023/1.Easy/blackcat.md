---
title: "BlackCat"
date: 2023-10-25T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Easy']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/discord_snowflake_scramble)  <

### We've been hit by the infamous BlackCat Ransomware Group! We need you to help restore the encrypted files. Please help! My favorite rock got encrypted and I'm a wreck right now!

Here we are given the file 'blackcat.7z' to download and inspect. Once unzipped, we find a folder with some encrypted files, a decryptmyfiles.exe, and a ransom note:

![blackcat1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcat1.png?raw=true)

If we run the binary, we are given a script which asks us to enter the decryption key: 

![blackcat3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcat3.png?raw=true)

It would be very difficult to guess the key at this stage, however after trying some fuzzing we noticed that the key needed to be at least 8 characters long otherwise, the script would exit without decrypting anything.

We began decompiling the binary in [Ghidra](https://ghidra-sre.org/) to gain a better understanding of what the binary is doing, and eventually came across an interesting file path:


![blackcat2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcat2.png?raw=true)

We know that the author, HuskyHacks, has a cat named Cosmo. So we decided to try 'cosmowar' and noticed that the decrypted output was almost human-readable compared to other keys, so we begain fuzzing the rest of the key using 'cosmo' as the base and guessing the remaining three characters.

We eventually were able to guess the key and decrypt the flag!

![blackcat4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcat4.png?raw=true)

Ornery kitty....
