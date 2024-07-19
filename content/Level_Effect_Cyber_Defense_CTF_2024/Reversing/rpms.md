---
title: "RPMs to the Max"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Reversing','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Reversing](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/shortcut)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/mangled)

### This is an actual malware sample seen in the wild. It's been defanged but it retains a lot if its original indicators. Amidst those indicators, you guessed it, is the flag!

####  README - You can access the challenge binary from the Cyber Defense CTF Triage Workstation VM on our [hosted platform](https://training.leveleffect.com/courses/f4a9466f-edb0-42ff-bb0e-a95af2b05de5). You can also [download](https://github.com/Level-Effect/CyberDefenseCTF-Public/raw/main/Challenges/2024/Mangled/packed-flag.zip) The password is 1332be84250cf925039fa88d70cf81b2f2b1430069e773dfdc2a54eb95f2589d

For this challenge, we are given the file AppLaunch.exe to inspect.

If we dump the strings on this file, we will see that it was written in .net assembly. Also, running the file causes a window to pop up which says 'Hello There'.

Since this is written in .NET, we can decompile it using DNSpy. 

We can quickly see that the actual name of this binary is Proker.exe.
Doing some inspection of what this is doing, it seems to be a Discord token stealer, and a cryptostealer. However, if we look at the main Program, we can see where it is printing the message, as well as a StringDecrypt function:

![rpms_main](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/rpms_main.png?raw=true)

If we follow the string decrypt function, we find that it is pulling some base64 strings and using those to decrypt:

![rpms_decrypt_function](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/rpms_decrypt_function.png?raw=true)

Following the Arguments, we can see that the 'Message' value is the payload, as well as the 'IP' value, they are being base64 decoded, xored, and base64 decoded again.

![rpms_strings](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/rpms_strings.png?raw=true)


We can see that there are some operations being done on the IP first, which we can reverse by base64 decoding, then xor the result with the value "Stemmatous", and then base64 decode again:

![rpms_ip](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/rpms_ip.png?raw=true)

We can perform the same steps on the 'message' value, and retrieve the flag:

![rpms_flag](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/rpms_flag.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/shortcut)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/mangled)
