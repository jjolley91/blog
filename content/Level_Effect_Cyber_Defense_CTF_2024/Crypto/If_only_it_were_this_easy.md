---
title: "If Only it Were This Easy"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Cryptography','Warmups','Easy']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Crypto](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/base_level)

### Flag: 577ca2e5adb9dc46b44f668923055b238243f9b398c670584430e1e327141949ed345afce50fa4c9de130d3c331936cebd5104206a959daf74b9f15b68cfb193

#### Key: 00112233445566778899aabbccddeeff00112233445566778899aabbccddeeff

#### IV: 0102030405060708090a0b0c0d0e0f10


This one is pretty straightforward. We are given a key and IV, as well as an AES encrypted flag. We can just decrypt the flag using something like [Cyberchef](https://cyberchef.org/#recipe=AES_Decrypt(%7B'option':'Hex','string':''%7D,%7B'option':'Hex','string':''%7D,'CBC','Hex','Raw',%7B'option':'Hex','string':''%7D,%7B'option':'Hex','string':''%7D)), and then base64 decode the result.

![if_only](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/if_only.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/base_level)