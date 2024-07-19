---
title: "Mangled"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Reversing','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Reversing](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/rpms)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/cti/)

### Pack? Sure. Unpack? Well...

#### README - You can access the challenge binary from the Cyber Defense CTF Triage Workstation VM on our [hosted platform](https://training.leveleffect.com/courses/f4a9466f-edb0-42ff-bb0e-a95af2b05de5). You can also [download](https://github.com/Level-Effect/CyberDefenseCTF-Public/raw/main/Challenges/2024/Mangled/packed-flag.zip) the binary from our GitHub. The password is 00ae587e22a708b1b61d155acfc54152200587af0711c4de16a9e1bfbb922d7f

For this challenge, we are given a packed-flag.exe to investigate. 


First, we can check the packing method used using Detect It Easy. This tells us that the packer used was UPX.


![mangled_upx](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/mangled_upx.png?raw=true)

We can try to upx unpack this, but the operation fails and we get an error. Seeing this, we will need to manually unpack the binary in order to retrieve the flag. I found a very helpful and detailed guide to explain this [Here](https://kausrini.github.io/2021-06-20-unpacking-upx-manually/).

Essentially, we will be opening the binary using x64dbg, and manually stepping through until we see a jmp instruction with no condition, followed by a long series of null bytes. At that point we will set a break, and step over it once.

![mangled_jmp](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/mangled_jmp.png?raw=true)

After that, the binary will be unpacked, and we can dump the unpacked binary using Ollydump. However, at this point we will still be missing the imports. We can use Scylla to retrieve the imports by importing our dumped binary, and selecting the 'Fix Dump' option. After that you should end up with something like this:

![mangled_dumped](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/mangled_dumped.png?raw=true)

We can open the packed-flag_dump_64_SCY.exe in Ghidra and retrieve the flag:

![mangled_final](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/mangled_final.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/rpms)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/cti/)