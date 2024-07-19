---
title: "Catch the Bandit"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Medium','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/double_take)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/haystack)

### Can you catch the bandit and recover the flag?

#### WARNING - The binary in this challenge is benign but we advise to run it on a VM. Do not run this on your personal machine. Use a VM in the Level Effect CTF course or your own.

For this challenge we are given bandit.exe to download and work with.
We don't really get anything useful by running strings on the binary. We could do some more static analysis, but the intended method is dynamic as the flag is decrypted at runtime.

If we run the binary, nothing seems to happen. However, we can use Procmon and one of several filters:

> process name contains/is bandit.exe

> path contains flag.txt

These are a few examples. 


![bandit_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/bandit_1.png?raw=true)

We can quickly see that the flag.txt file is being repeatedly written and deleted to the path C:\Users\\%Username%\AppData\Roaming\flag.txt

All we need to do now is recover the file and retrieve the flag! There are many ways to do this but a simple method would be to simply suspend the bandit.exe process in ProcExplorer, and then simply open the file to retrieve the flag!

![bandit_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/bandit_2.png?raw=true)



## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/double_take)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/haystack)