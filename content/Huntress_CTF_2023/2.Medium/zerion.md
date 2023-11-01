---
title: "Zerion"
date: 2023-10-02T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/hot_off_the_press) 

### We observed some odd network traffic, and found this file on our web server... can you find the strange domains that our systems are reaching out to?

This one gave us a PHP file that was obfuscated using a few different techniques which we can glean by reading the file in a text editor to try to understand what it is doing:

We can see the operations being performed at the beginning of the code: 
![zerion1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/zerion1.png?raw=true)
```PHP
 $L6CRgr=array(base64_decode("L3gvaQ=="),base64_decode("eA=="),base64_decode(strrev(str_rot13($L66Rgr[1]))))
```
From this we know that we need to:
1. Use a Rot13 cypher
2. reverse the strings
3. Base64 decode 

There are a few different methods of getting to the answer here, however, I went to [CyberChef](https://cyberchef.org/) and uploaded the file and was able to get the flag like so:

![zerion2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/zerion2.png?raw=true)

Alternatively, you could modify the php script like so:
```PHP
<?php $L66Rgr=explode(base64_decode("Pz4="),file_get_contents(__FILE__)); $L6CRgr=array(base64_decode("L3gvaQ=="),base64_decode("eA=="),base64_decode(strrev(str_rot13($L66Rgr[1]))));echo implode(" ",$L6CRgr);$L7CRgr = "d6d666e70e43a3aeaec1be01341d9f9d";preg_replace($L6CRgr[0],serialize(eval($L6CRgr[2])),$L6CRgr[1]);exit();?>
```
adding the :
```PHP
echo implode(" ",$L6CRgr);
```
and then run the script in the command line, grepping for the flag and retrieve it like so:
```bash
php zerion | grep  flag 
```
Or if you want to get fancy:
```bash
php zerion | egrep -oE 'flag\{[0-9a-f]{32}\}'
```

![zerion2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/zerion3.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/hot_off_the_press) 