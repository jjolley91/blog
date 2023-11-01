---
title: "Dumpster Fire"
date: 2023-10-08T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/comprezz)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/chicken_wings) 

### We found all this data in the dumpster! Can you find anything interesting in here, like any cool passwords or anything? Check it out quick before the foxes get to it! 

For this challenge we are given 'dumpster_fire.tar.xz'.

We can extract the contents in the commandline with:
```bash
tar xJvf dumpster_fire.tar.xz
```

We are then presented with what looks like an entire linux system worth of directories. After some ls -la we find some interesting files in the directory:
```bash
home/challenge/.mozilla/firefox/bc1m1zlr.default-release
```

Logins.json stands out as an interesting file. If we cat the file, we see that the username and password are encrypted. We then noticed the file key4.db, which seems to contain the decryption keys.

We eventually managed to find a python script to decrypt firefox stored credentials [Here](https://github.com/unode/firefox_decrypt/blob/main/README.md)

### Note: This tool has not been fully vetted, use at your own risk.

After running the script in the directory we were able to retrieve the flag
```bash
python3 decrypt.py .   
```
![dumpster_fire](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/dumpster_fire.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/comprezz)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/chicken_wings) 