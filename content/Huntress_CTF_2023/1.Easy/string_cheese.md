---
title: "String Cheese"
date: 2023-10-02T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/notepad) <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/query_code) 

### Oh, a cheese stick! This was my favorite snack as a kid. My mom always called it by a different name though...

This one is also pretty straightforward. We are given an image file 'cheese.jpg' to download to begin this challenge.

We can view the file and confirm that it is, indeed, a picture of string cheese. 

However, We can also run the 'strings' command on the file and extract the text to look for anything interesting. To save time we can filter the result by using grep to look for 'flag'!

```bash 
strings cheese.jpg | grep flag
```

![string cheese](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/cheese.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/notepad) <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/query_code) 