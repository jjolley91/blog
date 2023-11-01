---
title: "I Won't Let You Down"
date: 2023-10-05T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Easy']
---
 
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/caesarmirror)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dialtone) 

### OK Go take a look at this IP:
#### Connect here: http://155.138.162.158 # USING ANY OTHER TOOL OTHER THAN NMAP WILL DISQUALIFY YOU. DON'T USE BURPSUITE, DON'T USE DIRBUSTER. JUST PLAIN NMAP, NO FLAGS!

Obviously, the name of this challenge is a reference to "[I Won't Let You Down](https://www.youtube.com/watch?v=dQw4w9WgXcQ "test")" by OK Go! Upon visiting the link we are shown a music video and advised to watch until the very end. While listening to the video, we decided to run an nmap scan of the ip address, since the tip for the challenge indicated this might be the way to go.

```bash
nmap -sCV 155.138.162.158
```

From the Nmap results we can see that there is another http port open on 8888, as well as some other open ports that we decided to check out later, which didn't end up being required.

![lyd1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lyd1.png?raw=true)


Once we visit the URL on port 8888, the page begins printing the lyrics to the song, and gives us the flag at the end!

![lyd2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/lyd2.png?raw=true)


# flag{[here](https://www.youtube.com/watch?v=dQw4w9WgXcQ)}

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/caesarmirror)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dialtone) 
