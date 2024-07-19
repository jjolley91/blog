---
title: "Et tu, Brute?"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Networking','Easy']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Networking](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/signed_and_secured)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/drip_drop)

### Suspicious traffic has been seen on our company web server. Can you figure out the type of attack and find the flag?

### The flag in this one is not in the usual leveleffect{FLAG} format. You'll know it when you find it. When you do, submit it in the format leveleffect{INSERT_FLAG_HERE}


For this one, we are given http-traffic.pcap to download and inspect. Upon investigation, we find a bunch of http requests and they seem to be following a pattern of post/response. Inspecting a few of the post requests seems to indicate a brute force login attempt. If we look at the response codes, we can see they are mostly all 401- Unauthorized. We can filter those out and are left with a much shorter list:
> http.response.code!=401

From the result, we can see one that stands out is the one with the 302- Found response. Following the stream from there gives us the flag in the password field. We can wrap it in the leveleffect{} wrapper as instructed and submit the flag.

![et_tu_brute](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/et_tu_brute.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/signed_and_secured)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/drip_drop)

