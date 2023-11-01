---
title: "Speakfriend"
date: 2023-10-20T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/operation_eradication)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/rat) 

### It seems like this website was compromised. We found this file that seems to be related... can you make any sense of these and uncover a flag?

For this challenge, we are given a file 'main.7z' to download and extract, as well as a webserver to spin up. Once extracted we find that the file is an ELF64-bit binary (we see what you did there). We decided to deompile the binary using [Ghidra](https://ghidra-sre.org/) and found it was using curl to access the webserver, as well as some interesting variables containing hex:

```hex
0x2f616c6c697a6f4d
0x6562333920302e35
0x3762372d62353464
0x392d373930342d30
0x346138392d393732
0x6533353330666561
```

![speakfriend1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/speakfriend1.png?raw=true)


Once we decoded the hex, we retrieved a user agent string, and after some tinkering with the various curl options, we were able to curl the webserver with the decoded user agent string and retrieve the flag! 

```bash
curl -k -L -A 'Mozilla/5.0 93bed45b-7b70-4097-9279-98a4aef0353e' https://chal.ctf.games:32313
```


![speakfriend2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/speakfriend2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/operation_eradication)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/rat) 
