---
title: "Opposable Thumbs"
date: 2023-10-14T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/snake_eater)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/land_before_time) 

### We uncovered a database. Perhaps the flag is right between your fingertips!

For this challenge, we are given a thumbcache_256.db file to download and work with.

A "thumbcache_256.db" file is part of the Windows operating system and is associated with the thumbnail cache. Thumbnail caches are databases that store small, low-resolution versions of image and video files. These cached thumbnails are used by Windows to quickly display file and folder icons in File Explorer, as well as in various other parts of the user interface.  

All we need to do to view the contents of this file is to use a tool [thumbcache viewer](https://thumbcacheviewer.github.io/) which can be downloaded from github. Once you download the thumbcache_viewer.zip you can extract it, and run the executable. Then select file > open > thumbcache_256.db and the contents will be visible. Finally, all that is left to do is go to file > save all and you will be able to read the flag from the extracted .jpg!

![thumb](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/thumb1.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/snake_eater)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/land_before_time)