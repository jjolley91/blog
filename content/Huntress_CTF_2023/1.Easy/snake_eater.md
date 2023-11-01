---
title: "Snake Eater"
date: 2023-10-12T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/vbe)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/opposable_thumbs) 

### Hey Analyst, I've never seen an executable icon that looks like this. I don't like things I'm not familiar with. Can you check it out and see what it's doing?

For this challenge, I used a Windows 10 vm to download the file 'snake_eater.7z'
The first step is to extract the zipped archive, which will give us the snake_eater.exe to work with. 

Since this is a compiled binary you could go about analyzing this in a few different ways. We chose to use the dynamic analysis route. We initially tried analyzing this using Process Explorer, and checked autoruns but found nothing resembling a flag using those tools. We even checked wireshark to see if the malware was doing anything over the network, but again came up empty handed. Eventually We were able to retrieve the flag by inspecting its activity using Process Monitor with the following filters:

```txt
Process Name is snake_eater.exe
```
and later refined it with
```txt
Path contains flag
```
With those filters set, and Procmon capturing data we again ran the executable, and were able to retrieve the flag!

![snake_eater](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/snake_eater.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/vbe)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/opposable_thumbs)
