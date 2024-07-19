---
title: "Double Take"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/snake_in_my_boot)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/catch_the_bandit)

### I'm sure this image is hiding something, but nothing stands out no matter how I look at it. Maybe it's just stringing me along...

For this challenge we are given doubletake.jpg to download and inspect.
The trick to get the flag for this one is that you need to run the strings command specifically with the flags to look for 16-bit littleendian, and then base64 decode the result:

```bash
strings -e l doubletake.jpg | base64 -d
```

![doubletake](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/doubletake.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/snake_in_my_boot)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/catch_the_bandit)