---
title: "BaseFFFF+1"
date: 2023-10-04T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/human_two)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/caesarmirror) 

### Maybe you already know about base64, but what if we took it up a notch? 65535

Here we are given a text file 'baseffff1' to download. Opening the file in a text editor reveals what looks like some wierd characters. In fact, we are given a hint in both the title of the challenge and the name of the file that this is encoded in some way. In the hexadecimal system, there are 16 different digits, from 0 to 9 and A to F, representing values from 0 to 15. "FFFF" consists of four "F" characters, which in hexadecimal represent the value 15. Each position in the number represents a power of 16.

So, when you have "FFFF" in hexadecimal:

The first "F" represents 15 * 16^3 (15 times 16 to the power of 3, which is 40960).\
The second "F" represents 15 * 16^2 (15 times 16 to the power of 2, which is 3840).\
The third "F" represents 15 * 16^1 (15 times 16 to the power of 1, which is 240).\
The fourth "F" represents 15 * 16^0 (15 times 16 to the power of 0, which is 15).\
When you add these values together:

40960 + 3840 + 240 + 15 = 65535 

Then we just add the 1 at the end to get a final value of 65536.

Conveniently, there is actually an online tool that can decode base65536 [Here](https://www.better-converter.com/Encoders-Decoders/Base65536-Decode).

Once you paste in the message it is decoded and we receive the flag:

![baseffff+1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/baseffff+1.png?raw=true)  

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/human_two)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/caesarmirror)