---
title: "Where am I?"
date: 2023-10-09T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'osint', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/backdoored_splunk)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/operation_not_found) 

### Your friend thought using a JPG was a great way to remember how to login to their private server. Can you find the flag?

Here we are given a .png to download.
If we open the image, we see that it is a picture of a city skyline. We can try inspecting the metadata of the image to see if there is anything useful to be found using exiftool. ExifTool is a powerful and versatile command-line tool used for reading, writing, and editing metadata information in various types of files, primarily image and multimedia files. It can be installed like so:
```bash
sudo apt-get install libimage-exiftool-perl
```
and then inspect the file with the command:
```bash
exiftool PXL_20230922_231845140_2.jpg
```
Inspecting the output from the command we find some base64 encoding in the Description, and are able to decode that and retrieve the flag!

![where_am_i](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/where_am_i.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/backdoored_splunk)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/operation_not_found) 

