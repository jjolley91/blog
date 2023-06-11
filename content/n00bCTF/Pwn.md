---
title: "n00bCTF Pwn challenges"
date: 2023-05-25T13:25:32-05:00
tags: ['n00bCTF','Writeups', 'Pwn']
---
 
# [home](https://jjolley91.github.io/blog)

 # Intro

 These are the solutions I was able to find under the Web category. 

### Flag Shop

Prompt:
```
Come and buy yourself a flag! 
```
 We are given a netcat command to run the program:
 ```bash
 nc challs.n00bzunit3d.xyz 50267
 ```

We are told that we have 100 dollars, which is enough to buy 2 fake flags, but not enough to buy the real one.

```bash
Welcome to the flag shop! The flag costs $1337 but you have $100. You can buy the fake flag which costs $50
[1] Buy real flag - $1337
[2] Buy fake flag - $50
[3] Check account balance
```

However, we seem to be able to buy more than 2 of the fake flag:

```bash
[1] Buy real flag - $1337
[2] Buy fake flag - $50
[3] Check account balance
2
How many? 
1337
```
if we now check our balance we see that we have negative money left??

```bash
[1] Buy real flag - $1337
[2] Buy fake flag - $50
[3] Check account balance
3
$-66750
[1] Buy real flag - $1337
[2] Buy fake flag - $50
[3] Check account balance
```

The program does not seem to care that the value is negative, as long as it is greater than the price of the flag. we are now able to purchase the real one!

```bash
[1] Buy real flag - $1337
[2] Buy fake flag - $50
[3] Check account balance
1
How many? 
2
n00bz{5h0p_g0t_h3ck3d_4nd_fl4g_g0t_570l3n!}
```

```
Flag: n00bz{5h0p_g0t_h3ck3d_4nd_fl4g_g0t_570l3n!}
```
