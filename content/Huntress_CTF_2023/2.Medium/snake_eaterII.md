---
title: "Snake Eater II"
date: 2023-10-29T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/mfatigue)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/) 

### Snake Eater II - Revenge of the Snake Eater

### The Threat Actor must have gotten word that you had no trouble dissecting Snake Eater. They said this one is a bit more... involved.

For this challenge, we are given snake_eaterII to download, and inspect. We recalled from the first snake eater challenge, we were able to find the flag using Process monitor, so we decided to start there to see if there was anything interesting to find. We loaded up Process Monitor with the following filters:

```txt
Process Name is snake_eaterII.exe
```
and
```txt
Path contains flag
```
We observe similar behavior to the first snake_eater, however, this time the flag is being written to a file which was created in a random directory (usually somewhere in the C:\Users\user\AppData\Roaming\ path) and then being deleted before the program terminates.

We attempted to use x64dbg to step through the binary and pause the program after it had written the flag, but before it was able to delete it, but we eventually realized that we could simply use a tool to recover the deleted file.

We ran the program while watching process monitor for the exact path for the flag, then used [Recuva](https://www.ccleaner.com/recuva/download/standard) to recover the deleted file and retrieve the flag!

![snake_eaterii](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/snake_eaterii.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/mfatigue)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/) 
