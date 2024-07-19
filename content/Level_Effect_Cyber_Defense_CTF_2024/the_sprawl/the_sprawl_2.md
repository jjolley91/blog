---
title: "The Sprawl 2"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','osint','Forensics','Cryptography','Medium','Hard']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [The Sprawl](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/the_sprawl/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/the_sprawl/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/)

#### For these challenges we will be working with theSprawl2.exe

#### README - You can access the challenge binary from the Cyber Defense CTF - 2nd Phase Triage Workstation VM on our [hosted platform](https://training.leveleffect.com/courses/2a4dccb7-3d5b-4312-816e-ef3728d25b67). You can also [download](https://github.com/Level-Effect/CyberDefenseCTF-Public/raw/main/Challenges/2024/The%20Sprawl2/theSprawl2.zip) the binary from our GitHub.

#### WARNING - This challenge has malware-like behavior involved. DO NOT run this on your personal machine. Use a VM in the Level Effect CTF course or your own.


## Sprawl2 Part 1 - The Shapeshifter Enters (Medium)

### When you engaged with the virulent Sprawl2.exe program, who were you this time?

When we run this binary, we get an identity check failed message, at which point kitsune casts Powerball on the binary and the program terminates. 

We can dump the strings on the binary, and scrolling through, we see a string: ```kitsunekitsunekitsunekitsune4444```, if we pass this in as an argument when we run the binary, we get the first flag! (It was also visible in the strings dump)

##### Note: This flag needed to be put inside the leveleffect{} wrapper to be accepted.

![sprawl_2_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sprawl_2_1.png?raw=true)

## Sprawl2 Part 2 - Help is Provided (Medium)

### Casting spells together make them much stronger. Combine what you know of from both that were cast and decrypt the helper message.


I dont think I solved the rest of these in the intended way, but I will go through my process regardless.

For the second and third challenge, I decompiled the binary in Ghidra, and found the next two flags inside the strings: 

![sprawl_2_2_and_3_flags](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sprawl_2_2_and_3_flags.png?raw=true)
## Sprawl2 Part 3 - Delete Soul (Hard)

### At this point you should be familiar with who you are dealing with. Look up what they want to ultimately achieve. You have a hint on how to configure it by now if you decrypted the previous message.

Same as above for this one, The flag was in the strings I found inside Ghidra:

Also of note, these were present in the strings dump of the binary, I just didnt look for them...

![sprawl_2_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sprawl_2_3.png?raw=true)


## Sprawl2 Part 4 - Memories of it All (Hard)

### Were you really the shapeshifter all along? or did you help as someone else without knowing? either way - it's a memory now.

Still looking in Ghidra, we see some hex strings being concatenated:

![sprawl_2_4_hex](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sprawl_2_4_hex.png?raw=true)


we can decode these, and reverse them, and piece them back together to retrieve the final flag:

![sprawl_2_4_decode](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sprawl_2_4_decode.png?raw=true)

##### Note: This flag needed to be put inside the leveleffect{} wrapper to be accepted.

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/the_sprawl/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/)