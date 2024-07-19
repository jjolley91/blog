---
title: "Signed and Secured"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Networking','Easy','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Networking](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/ask_and_rcv_1_2_3)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/et_tu_brute)

### We have intercepted some network traffic after an alert hit from our SOC. Something seems off about some of the traffic here, but we haven't found anything concrete yet...


Here we are given a file to download; suspicious.pcap.

Upon inspection, we can see some http traffic. However, these only lead to dead ends. If we take the name of the challenge as a hint, or just dig around for a while, we will eventually find some tls handshakes. Drilling down into those will show one is an obviously bogus certificate, and the flag can be found in the id-at-stateOrProvinceName field.


Filter:
> tls.handshake.type==11

![signed_and_secured](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/signed_and_secured.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/ask_and_rcv_1_2_3)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/et_tu_brute)