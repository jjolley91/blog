---
title: "Magic_repairman"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Easy']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/thats_epoch)

### You'll probably need some tools to fix this one. Hexedit, HxD or hexed.it are commonly used.

Here we are given a file to download 'magic_repairman.png'. If we try to open the file from the start we get an error message telling us the file is corrupted.

We can take the advice in the prompt and open the imagewith a hex editor:

> hexedit magic_repairman.png

![magic_repairman_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/magic_repairman_1.png?raw=true)


If you are familiar with file headers, we can easily spot the header here is incorrectly showing .RNG instead of .PNG. We can simply look up the hex code for a capitol 'P' and change the value in the hexeditor. Here is a [site](https://www.freecodecamp.org/news/ascii-table-hex-to-ascii-value-character-code-chart-2/) with the table.   

We will quickly see that the code for R is 52, and it needs to be changed to 50. We can save our changes and then view the flag in the image!


![magic_repairman_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/magic_repairman_2.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/forensics/thats_epoch)