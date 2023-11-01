---
title: "lolz#4"
date: 2023-10-13T13:11:20-10:01
#draft: true
tags: ['CTF', 'Writeups', 'Impossible Difficulty', 'Extreme']
---
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Impossible Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/3.Hard/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz3)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz5) 

* Please note that this challenge was a community effort and much of the content in this writeup is attributed to findings from the public discourse.

### I'm starting with the man in the mirror.

The challenge provides an attachment named image_3.png, a picture featuring Rick Astley in a mirror. The challenge text and image are hints to look at the previous challenge "I Won't Let You Down" which featured a rick roll on a hosted server. A user in the community discovered a location on the server `http://155.138.162.158/mirror` which displayed the hint:

```txt
The answer was in front of you the first time I let you down.
```

Going back to the challenge entry for "I Won't Let You Down" and inspecting it in devtools, we found a hidden URL titled "mirror".

![lolz4_1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz4_1.png?raw=true)


The link led to an interactive site featuring a bunch of red herrings and Rick Astleys.

![lolz4_2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz4_2.png?raw=true)

Some elements on the site were interesting to investigate, namely all the images of fish and Rick Astley and some obfuscated JavaScript in the source. In the end, though, all of these turned out to be red herrings as the point of interest was a fake favicon, spotted due to its unusually large file size.

![lolz4_3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz4_3.png?raw=true)

We downloaded the favicon and discovered that it's actually a JPEG.

![lolz4_4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz4_4.png?raw=true)

After trying a number of steganography extraction tools, we were eventually successful with the steghide cracker [StegSeek](https://github.com/RickdeJager/StegSeek) using rockyou.txt as the wordlist. Viewing the extracted file gave us the flag!

![lolz4_5](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz4_5.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz3)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz5) 