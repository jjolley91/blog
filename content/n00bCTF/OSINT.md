---
title: "n00bCTF OSINT challenges"
date: 2023-05-25T13:25:32-05:00
tags: ['n00bCTF','Writeups', 'osint','CTF']
---
 
# [home](https://jjolley91.github.io/blog)

 # Intro

  These are the solutions I was able to find under the OSINT category. 


  ### Damn

Prompt:
```
Damn bro, Dam! -- Note: Find out the city that this dam is in. Flag format is n00bz{City_Name} 
```
 We are given dam.png to download.

 ![dam](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/dam.png?raw=true)

 I put this image into Google image search to see if I could find the location.

 Searching for the image source I was able to find an article about Kakhovka dam collapse oin Ukraine.

 https://www.theguardian.com/world/2023/jun/09/visual-guide-ukraine-nova-kakhovka-dam-collapse

![Ukraine_map](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/Ukraine_map.png?raw=true)

```
Flag:  n00bz{Nova_kakhovka}
```

