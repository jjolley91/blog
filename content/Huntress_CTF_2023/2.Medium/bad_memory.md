---
title: "Bad Memory"
date: 2023-10-24T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/batchfuscation)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/mfatigue) 

### A user came to us and said they forgot their password. Can you recover it? The flag is the MD5 hash of the recovered password wrapped in the proper flag format.

For this challenge we are given a 600MB file 'image.zip' to download, which contains the image.bin, a memory dump, from which we need to recover the password. To do this, we can use a tool called [volatility 3](https://github.com/volatilityfoundation/volatility3) to dump the NTLM hashes for the users.  

Volatility is a powerful memory forensics tool used to analyze memory dumps from running systems. When analyzing a memory image (image.bin), you can use Volatility to extract NTLM hashes from it using various plugins. NTLM (NT LAN Manager) hashes are commonly used for authenticating users in Windows environments.

```powershell
vol.py -f ../image.bin windows.hashdump.Hashdump
```
The output will look like this, and we can see the user 'congo' stands out as a non default user on the system:  

![bad_memory3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/bad_memory3.png?raw=true)


We can copy the nthash value for this user and try our luck cracking it easily using [crackstation](https://crackstation.net/). Sure enough, it is able to crack the hash!


![bad_memory1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/bad_memory1.png?raw=true)


The challenge says to get the flag, we need the md5sum of the password wrapped in the standard flag format, so we can do that and retrieve the flag!

![bad_memory2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/bad_memory2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/batchfuscation)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/mfatigue) 
