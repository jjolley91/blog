---
title: "Traffic"
date: 2023-10-04T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Medium']
---
 

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/hot_off_the_press)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/backdoored_splunk) 

### We saw some communication to a sketchy site... here's an export of the network traffic. Can you track it down?

#### Some tools like rita or zeek might help dig through all of this data!

Here we are given 'traffic.7z' to download and extract.

For this challenge, we used [Rita](https://github.com/activecm/rita). Once you get Rita installed, you just need to 
```bash
gunzip ./*
```

The files and load them into rita dataset, then create a web report with:

```bash
./rita html_report
```

If we look under Beacons SNI, we see a site that looks suspicious:

![traffic1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/traffic1.png?raw=true)

Visiting the sketchy site we can retrieve the flag!

![traffic2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/traffic2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/hot_off_the_press)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/backdoored_splunk) 


