---
title: "Haystack"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Medium','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/catch_the_bandit)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/motw)

### The flag is in here somewhere...

For this challenge, we are given haystack.zip to download.

The zip folder contains nested directories, each containing 100 txt files named flag.txt, all but one file contains a fake flag.

If we cat out a few of the flags we see that all of the fake flags are the same hex and base64 encoded {fakeflag}. This makes it easy, and we can retrieve the real flag with a simple bash command:
```bash
grep -Rv '39 6d 62 47' haystack | cut -d':' -f2 | xxd -r -p | base64 -d && echo
```


![haystack](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/haystack.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/catch_the_bandit)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/motw)