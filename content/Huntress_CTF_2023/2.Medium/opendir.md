---
title: "Opendir"
date: 2023-10-13T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/under_the_bridge)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/tragedy) 

### A threat actor exposed an open directory on the public internet! We could explore their tools for some further intelligence. Can you find a flag they might be hiding?

#### NOTE: This showcases genuine malware samples found a real opendir. For domain reputation purposes, this is behind Basic Authentication with credentials: opendir:opendir

Here we are given a webserver to interact with. Visiting the webpage, and entering the username and password, we find a list of files and one directory being hosted. The directory 'sir/' stood out right away, so we inspected that to start. This directory contained a number of other directories and executables, however again one stood out :'64_bit_new/' and we decided to check in there. Among the files in this directory there was one txt file, which we decided to open and do a search for 'flag{'. Sure enough, there it was!

![opendir1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/opendir_flg_1.png?raw=true)

We also decided to take a more streamlined approach to this and decided to download all the files with a simple wget command from linux:
```bash
wget -r --http-user=opendir --http-password=opendir http://chal.ctf.games:30014/
```
we then were able to retrieve the flag with a simple grep command:

```bash
grep -ri 'flag{'
```

![opendir1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/opendir_flg_2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/under_the_bridge)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/tragedy) 

