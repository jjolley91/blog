---
title: "Traffic"
date: 2023-10-04T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Medium']
---
 

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/hot_off_the_press)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/backdoored_splunk) 

### We saw some communication to a sketchy site... here's an export of the network traffic. Can you track it down?

#### Some tools like rita or zeek might help dig through all of this data!

Here we are given 'traffic.7z' to download and extract.

For this challenge, we used [Rita](https://github.com/activecm/rita).

I borked my linux vm and was unable to grab a screenshot for this one, once I get it back up I will come back and fix this writeup.

Overall, Once you get Rita installed, you just need to 
```bash
gunzip ./*
```

The files and load them into rita, then you can simply search for the flag!

![traffic](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/traffic.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/hot_off_the_press)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/backdoored_splunk) 


