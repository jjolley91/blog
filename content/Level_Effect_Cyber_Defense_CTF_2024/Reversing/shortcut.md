---
title: "Shortcut"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Reversing','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Reversing](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/flag_worthy)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/rpms)

### The key to solving this challenge is LNKing things together!

#### README - You can access the challenge binary from the Cyber Defense CTF Triage Workstation VM on our [hosted platform](https://training.leveleffect.com/courses/f4a9466f-edb0-42ff-bb0e-a95af2b05de5). You can also [download](https://github.com/Level-Effect/CyberDefenseCTF-Public/raw/main/Challenges/2024/Mangled/packed-flag.zip) The password is a5e17d51da43123dd1a27bf1001b58c0f721e6a17b31978146bdaf56f620e498

##### WARNING - This challenge has malware-like behavior involved. DO NOT run this on your personal machine. Use a VM in the Level Effect CTF course or your own.

For this challenge, we are given a flag.ps1 file and a GetFlag shortcut file to inspect.

The flag.ps1 contains some obfuscated powershell. After some deobfuscation we can see that it takes an input parameter, and is comparing the sha256 value against a hardcoded value. If it matches, it uses that as part of the key to aes decrypt the flag. It is also checking to see if there is an environment variable set to the hardcoded value, which base64 decodes to 'sesame'. If these conditions are met, the decrypted flag gets printed:

![shortcut1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/shortcut1.png?raw=true)

Honestly, I simply base64 decoded the environment variable and was able to guess the input value was supposed to be 'open'. However, you could also take the hash given and crack it using your method of choice. [Crackstation](https://crackstation.net/) would do the trick as well.

We can set our environment variable to the password in powershell using:

```ps
$env:P2 = "sesame"
```
and then run the flag.ps1 file with the input 'open' to retrieve the flag:


![shortcut2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/shortcut2.png?raw=true)



## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/flag_worthy)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/rpms)
