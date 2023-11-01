---
title: "lolz#3"
date: 2023-10-09T13:11:20-10:01
#draft: true
tags: ['CTF', 'Writeups', 'Impossible Difficulty', 'Extreme']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Impossible Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/3.Hard/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz2)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz4) 


* Please note that this challenge was a community effort and much of the content in this writeup is attributed to findings from the public discourse.

This challenge just provides the attachment bops_lang.wav to analyze. Using [this site](https://futureboy.us/stegano/decinput.html), we recovered embedded text from the file:
```txt
Pakitaan mo ng pagmamahal si Rick
```

This is Tagalog which translates to
```txt
Show Rick some love
```

Someone from the community realized from this hint that this challenge is tied to the previous challenge "I Won't Let You Down" which featured a rick roll on a hosted server. They found an image located on that server named love. Running `wget 155.138.162.158/love` retrieves the PNG, shown below.

![lolz3_1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz3_1.png?raw=true)

Despite the image claiming it's a red herring, it's actually the answer. Suspecting more steganography at play, we ran zsteg against the image and successfully extracted the flag!

![lolz3_2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lolz3_2.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz2)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/4.impossible/lolz4) 