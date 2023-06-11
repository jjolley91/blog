---
title: "n00bCTF Forensics challenges"
date: 2023-05-25T13:25:32-05:00
tags: ['n00bCTF','Writeups', 'forensics']
---
 
# [home](https://jjolley91.github.io/blog)

 # Intro

 # Intro
These are the solutions I was able to find under the Forensics category.


### Crack & Crack

Prompt: 

```
Just Crack & Crack!
```

Here we are given a flag.zip to download. 

Once downloaded, we can see that the file is password protected.

I decided to take this to John (the ripper) to try to crack the password

```bash
zip2john flag.zip > flag.txt
```
```bash
john --wordlist=rockyou.txt flag.txt
```
It found the password!

```
password: 1337h4x0r
```

I then unziped the file and found flag.pdf...which is also password protected

JOHNNNNNNN

```bash
pdf2john.pl flag.pdf > flag.txt  
```
```bash
john --wordlist=rockyou.txt flag2.txt
```
I was able to retrieve the password for the pdf now!
```bash
john --show flag2.txt
```
```
password: noobmaster
```
```
Flag: n00bz{CR4CK3D_4ND_CR4CK3D_1a4d2e5f}
```
