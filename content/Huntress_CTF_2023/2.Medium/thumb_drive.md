---
title: "Thumb Drive"
date: 2023-10-19T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/indirect_payload)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/operation_eradication) 

### People say you shouldn't plug in USB drives! But I discovered this neat file on one that I found in the parking lot...


In this challenge, we are given a file 'ADATA_128GB.lnk' file to download.

A ".lnk" file, also known as a Windows shortcut, is a file that points to another file or resource on a Windows operating system. It is used to provide a convenient way to access programs, files, directories, or network resources without having to navigate through the entire file system. When you double-click a .lnk file, it typically opens the linked resource.
We used lnkparse for the first step, which can be installed on linux using:
```bash
pip3 install lnkparse
```
If we use the tool 'lnkparse' we can extract the following link from the file:
```bash
lnkparse -a ADATA_128GB.lnk
```
tinyurl.com/a7ba6ma which we can expand using [urlscan.io](https://urlscan.io/) to get a link to a google drive file 'usb.txt'

![thumbdrive1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/thumbdrive1.png?raw=true)


The text file contains some encoded data, and after some trial and error, we found that it was encoded with base32. We new we were on the right track when we could make out the MZ headder indicating that this will be a windows PE file.    

We downloaded that file, and figured out that this was a dll that we could run by calling rundll32 like so:
```powershell
rundll32.exe .\hello-world.dll, main
```
The program will error, but we still get the flag!

![thumbdrive2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/thumb_drive_flag.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/indirect_payload)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/operation_eradication) 