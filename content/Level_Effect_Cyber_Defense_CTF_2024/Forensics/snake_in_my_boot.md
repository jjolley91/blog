---
title: "There's A Snake in My Boot!"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Easy','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/thats_epoch)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/double_take)

### A classic game of Snake, but the developer left the winning flag in the binary a little too exposed.


Here we are given a file 'snek' to download. Inspecting the file reveals that it is an ELF 64 executable.
```bash	
chmod +x snek
```
we can run the binary now and see that it is, indeed, a small game of snake. If we run the game, and survive for 90 seconds, we get a message with a shortened link: 

```txt
Nice job getting this far, you're a pro! However, there is a shorter path to victory... https://rb.gy/7i3c9d
``` 
![snek_1](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/snek_1.png?raw=true)

If we look at the url, it does provide a hint into what the correct step to get the flag is...

```bash
strings snek | grep leveleffect
```

![snek_2](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/snek_2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/thats_epoch)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/double_take)