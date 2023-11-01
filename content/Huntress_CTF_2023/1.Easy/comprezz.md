---
title: "Comprezz"
date: 2023-10-08T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/layered_security)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dumpster_fire) 

### Someone stole my S's and replaced them with Z's! Have you ever seen this kind of file before? 
Here we are given a file "comprezz" to download and inspect. Running the file command on the file reveals that it is compressed in some way. We tried a few different ways of decompressing the file, and found that 7zip was able to successfully decompress the data.
```bash
7z x comprezz
```
We were then able to read the flag!

![comprezz](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/comprezz.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/layered_security)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dumpster_fire)