---
title: "Wimble"
date: 2023-10-10T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/chicken_wings)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/f12) 

### "Gretchen, stop trying to make fetch happen! It's not going to happen!" - Regina George, Mean Girls

For this challenge we are given a file 'wimble.7z' to download.  
Once we extract the archive, we are given the file 'fetch'. If we inspect the fetch file, we find it is another compressed file which we can extract to receive a bunch of files with the .pf extension.   

![wimble1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/wimble.png?raw=true) 


The .pf extension is typically associated with "Windows PreFetch" files. These files are used by the Windows operating system to improve the startup performance of applications. We can use one of [EricZimmerman's tools](https://github.com/EricZimmerman/Prefetch/tree/master/Prefetch), prefetch. This tool is designed to work with Windows Prefetch files to provide forensic investigators and analysts with valuable information about a Windows system's application execution history. The tool can help in various investigative scenarios, including incident response and digital forensics. If we use [PECmd.exe](https://github.com/EricZimmerman/PECmd?search=1) in powershell on the folder we extracted from the fetch archive, we can include a findstring and retrieve the flag! 

```powershell
.\PECmd.exe -d . | findstr.exe /i 'flag'
```


![wimble2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/wimble_flag.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/chicken_wings)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/f12) 