---
title: "M Three Sixty Five"
date: 2023-10-16T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/land_before_time)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/press_play_on_tape) 

### Connect with SSH, with username user and SSH password userpass. Your syntax may look like: ssh user@chal.ctf.games -p [PORTNUMBER]

This challenge contains 4 total flags which are all in the same box. We are given ssh login credentials to access a Powershell core instance. Powershell is very helpful for this, as all you need to do to find the commands you need to use is ask it using 
```powershell
get-help
```

#### Note: These do not need to be solved in a specific order  

### Challenge 1: Welcome to our hackable M365 tenant! Can you find any juicy details, like perhaps the street address this organization is associated with?


![m_365_1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/m_365_1.png?raw=true)


### Challenge 2: This tenant looks to have some odd Conditional Access Policies. Can you find a weird one?

![m_365_2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/m_365_2.png?raw=true)


### Challenge 3: We observed saw some sensitive information being shared over a Microsoft Teams message! Can you track it down?

![m_365_3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/m_365_3.png?raw=true)


### Challenge 4: One of the users in this environment seems to have unintentionally left some information in their account details. Can you track down The President?

![m_365_4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/m_365_4.png?raw=true)


This just goes to show, the only command you need to know in powershell is 'Get-help'.

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/land_before_time)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/press_play_on_tape) 