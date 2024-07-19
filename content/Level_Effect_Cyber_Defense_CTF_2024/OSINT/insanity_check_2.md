---
title: "Insanity Check - 2"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','osint','Easy', 'Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Osint](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/insanity_check_1)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/git_em)

### You know the deal - join the disc, make sure your eyes work, don't go crazy.

### Did you make sure there were no other flags in the Discord?


This one seemed to be unexpecedly tricksey for many. If we follow the same steps from before, but this time in the [cyber-defense-ctf](https://discord.com/channels/755445294052933632/1250488991883591740) channel, we will find the very first comment actually contains a thread named "Well what's this....👀" and we can see the flag posted there by an admin:

![insanity_check_2_1](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/insanity_check_2_1.png?raw=true)


Except oh wait, that is not a real flag! To find the actual flag you need to copy the text of the message like so: 

![insanity_check_2_2](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/insanity_check_2_2.png?raw=true)

and paste it somewhere. You will then see that the message is actually very long, and was being truncated by discord: 

```👀 False flag: leveleffect{s1LLy_G00s3_th1s_1s_n0t_@_fl@g} ~~‎~~||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​||||​|||||||||||| leveleffect{this was the real flag}```


Pretty clever!

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/insanity_check_1)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/git_em)