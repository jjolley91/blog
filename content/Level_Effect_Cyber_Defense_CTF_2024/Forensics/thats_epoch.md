---
title: "That's Epoch"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Warmups','Easy']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/magic_repairman)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/snake_in_my_boot)

### Learning about the Y2K38 problem will lead you to a way to decode the flag. 1721387471

#### The flag is in the format leveleffect{dd MMMM yyyy HH:mm:ss}

For this challenge we simply need to convert the given epoch timestamp into it's UTC format. We can easily do this in bash:
```bash
date -u -d @1721387471
```

![thats_epoch](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/thats_epoch.png?raw=true)

Simply wrap the flag in the leveleffect{} wrapper in the way described and that's it!


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/magic_repairman)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/snake_in_my_boot)