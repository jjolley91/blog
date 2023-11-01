---
title: "Layered Security"
date: 2023-10-07T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/php_stager)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/comprezz) 

### It takes a team to do security right, so we have layered our defenses!

For this challenge, we are given a file 'layered_security' to download.
If we run the file command on it we can see the following info:

```bash
layered_security: GIMP XCF image data, version 011, 1024 x 1024, RGB Color
```
So we can immediately tell that it is an image in the GIMP image format. Regarding the GIMP image format, GIMP uses its own native file format, which is known as XCF (eXperimental Computing Facility). XCF is the default file format for saving images in GIMP. It is a flexible format that preserves layers, channels, paths, and other image editing information, making it ideal for working on complex projects with multiple layers and edits.

We can install the tool using:
```bash
sudo apt install gimp
```
and then inspect the file with the command
```bash
gimp layered_security
```

We can see that this is a series of AI generated faces which are all layered on top of one another. We can then begin hiding the layers one by one until we come to the image with the flag:


![layered](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/layered.png?raw=true)



From here, you can either manually enter the flag, or take a screenshot and submit it to an online text extractor such as [this one](https://www.imagetotext.info/) that worked for us.

![layered](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/layered2.png?raw=true)



## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/php_stager)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/comprezz) 