---
title: "Human Two"
date: 2023-10-03T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/book_by_its_cover)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/baseFFFF+1/) 

### During the MOVEit Transfer exploitation, there were tons of "indicators of compromise" hashes available for the human2.aspx webshell! We collected a lot of them, but they all look very similar... except for very minor differences. Can you find an oddity? 

Here we are given a zip file to download. Once unzipped we are given a ton of html text documents and the objective here is to find which one contains the flag.

All of the file sizes are exactly the same, however, using:``` diff``` on two of the files reveals that line 36 is different between all of the files.

#### Example: 
![human_two1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/human_two1.png?raw=true)


We can then grep for 'pass' on that line to  identify anything that stands out:
```bash
grep pass *
```
scrolling through we find that one stands out and is much longer than the others:
```bash
cc53495bb42e4f6563b68cdbdd5e4c2a9119b498b488f53c0f281d751a368f19:    if (!String.Equals(pass, "666c6167-7b36-6365-3666-366131356464"+"64623065-6262-3333-3262-666166326230"+"62383564-317d-0000-0000-000000000000"))
```
We can then decode the hex values from this to retrieve the flag. Here is another fancy one liner to do it all in one go:

```bash
grep pass * | grep -v var | egrep -E '.{200,}' | egrep -oE '\"([0-9a-f+"-]+)\"' | tr -d '"' | xxd -r -p
```

![human_two](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/human_two.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/query_code)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/baseFFFF+1/) 