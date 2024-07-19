---
title: "In the System"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Log_analysis','Easy','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Log_analysis](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Log_analysis/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Log_analysis/whoami)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/)

### An analyst noticed some suspicious account activity on a workstation. We think the device may be compromised – can you look into this?


For this challenge, we are given log_chall.evtx to download and investigate.

We can open the file using Event viewer. You will notice right away that  all of the event ID's are 4624 logon events.

We can simply use the 'Find' command to filter for leveleffect, and it will take us to the log with the flag in the TargetUserName field.

![in_the_system](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/in_the_system.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Log_analysis/whoami)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/)