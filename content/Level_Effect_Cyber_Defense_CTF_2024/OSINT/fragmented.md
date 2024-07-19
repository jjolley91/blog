---
title: "Fragmented"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','osint','Easy','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Osint](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/inspector)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/shameless_plug)

### It's a good habit to be suspicious of shortened links, but this one might be worth looking at a little more closely...

https://bitly.cx/DwjQc

Here we are given a shortened bitly link, which goes to a cooking site. You can either visit the site, or use a url unshortener such as [this one](https://unshorten.net/). You will notice at the end of the url a '\#'followed by a string. This is called a url Fragment Identifier, and it points to a specific section or element within a given webpage. However, if the fragment is invalid, it is simply ignored. 

![fragmented1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/fragmented1.png?raw=true)

In this case, the fragment contains a string which is base64 encoded:

 ```bGV2ZWxlZmZlY3QlN0I2NjcyMzQ2NzZkMzM2ZTc0MzUlN0Q=```

The rest can be most conviniently done using [CyberChef](https://cyberchef.org/)

First, we decode the base64, then url decode. The result seems to be a valid flag, however there is still the last part to decode, inside the curly brackets we have some hex that needs to be decoded to get the final part of the flag.

![fragmented2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/fragmented2.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/inspector)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/osint/shameless_plug)