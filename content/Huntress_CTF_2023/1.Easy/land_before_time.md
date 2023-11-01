---
title: "Land Before Time"
date: 2023-10-14T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Steganography', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/opposable_thumbs)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/m_three_sixty_five) 

### This trick is nothing new, you know what to do: iSteg. Look for the tail that's older than time, this Spike, you shouldn't climb. 

Here we are given an image to download 'dinosaurs1.png'. The tool we need for this is right in the challenge hint' isteg'. We initially tried using [Aperi'Solve](https://www.aperisolve.com/) to solve this. We uploaded the image, and extracted the zsteg files, and retrieved the flag...

![lbft1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lbt1.png?raw=true)


...Just kidding...the flag{f162b6973561877eaa124814ce1c721a} here was a phony, however the result also provided some potential passwords. We decided to try re-extracting the files using the password 'johnhammondiscool', and this time we were able to retrieve the flag...
![lbft2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lbt2.png?raw=true)


...Just kidding again..the flag:
```text
flag{eW91IGFjdHVhbGx5IHRob3VnaHQsIG5nbCBpdCdzIGZ1bm55IGxvbA==}
```
decoded to: 'you actually thought, ngl it's funny lol'

we also got a few links: [this](https://ctf4hire.com/favicon.ico), and [this](https://ctf4hire.com/), and [this one](https://www.youtube.com/watch?v=34Ig3X59_qA) was really interesting....

Also present was another base64 encoded message:
```
eW91IGZlbGwgZm9yIGl0IGFnYWluLCB4RCAKCi4KLgouCi4KLgouCi4KLgouCi4KLgouCi4KLgouCi4KLgouCi4KLgouCi4KLgouCi4KLgouCi4KCm5haGggSSBjYW4ndCBiZSBtZXNzaW5nIHdpdGggeW91CgpIZXJlIHRha2UgeW91ciBmbGFne2FIUjBjSE02THk5M2QzY3VlVzkxZEhWaVpTNWpiMjB2ZDJGMFkyZy9kajB6TkVsbk0xZzFPVjl4UVE9PX0=
```
decoded to:
```
you fell for it again, xD 

.
.
.
.

nahh I can't be messing with you

Here take your flag{aHR0cHM6Ly93d3cueW91dHViZS5jb20vd2F0Y2g/dj0zNElnM1g1OV9xQQ==}  
```
And finally we were able to...get trolled again. Nice.

By this point it became apparent that this online tool was not going to work, and we did, indeed, need to use the iSteg tool. After some searching, we were able to find a version of the tool hosted on [GitHub](https://github.com/rafiibrahim8/iSteg). we downloaded the GUI release, and ran the iSteg-v2.1_GUI.jar program which allowed us to finally retrieve the real flag! (no password required)

![lbftflag](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lbtf.png?raw=true)

#### This was an entertaining challenge, and I included all of the fake flags because I found them fun, as well as frustrating. Well played, proslasher, well played.

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/opposable_thumbs)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/m_three_sixty_five) 