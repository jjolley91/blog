---
title: "Git 'em"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','osint','Medium','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Osint](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/insanity_check_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/)

### We have observed conversations on an underground forum that indicate potential plans to target Goodcorp. Here's a snippet of the discussion. Can you find more information on these users and figure out their plan?
```
Шадоу
14:04 (22 minutes ago)
To jakearmitage1337

Чувак! Нафига ты такую инфу на всеобщее обозрение выложил! 
Быстро убери, пока вся операция не накрылась! 

----------------------------------------------------------

jakearmitage1337
14:09 (17 minutes ago)
To Шадоу

Сорян, босс! Проглядел. Уже убрал, так что всё норм.
```
For this challenge, we are given an intercepted communication, all we need however is the username to begin the investigation. If we take the name of the challenge as a hint we can quickly find a username that matches the one given as well as a repo:'SuperSecretProject'. We can read through some of the files and see their plan for goodcorp laid out, but no flag. If you translated the Russian you might learn that the 'critical information' has been removed. If we look at the commit history and go back to the first entry, sure enough we get the flag.

![git_em](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/git_em.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/insanity_check_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/)