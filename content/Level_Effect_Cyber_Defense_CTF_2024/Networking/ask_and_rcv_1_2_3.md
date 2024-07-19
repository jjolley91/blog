---
title: "Ask and You Shall Recv 1, 2, & 3"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Networking','Easy','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Networking](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/back_to_basics_1_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/signed_and_secured)

## Ask and You Shall Recv 1 

### Connect to port 24194 on 0.cloud.chals.io to get the flag.

To get the flag for this first challenge you simply need to connect to the webserver on the specified port:

> nc 0.cloud.chals.io 24194

![ask_and_recv_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ask_and_recv_1.png?raw=true)


## Ask and You Shall Recv 2

### Your goal is to SSH to 0.cloud.chals.io over port 21986 using the private key provided for download. The passphrase is cda-od.

### The username to connect with is the name of the operation led by law enforcement agencies in January 2021 that dealt a considerable blow to Emotet infrastructure.

#### Note - sharing private keys is always a bad idea - this is only for the purposes of the challenge.

Okay, so we know we simply need to ssh into the webserver as the prompt suggests. If we do a little bit of google research into the operation described in the prompt, we can quickly find the name of the operation [here](https://blogs.vmware.com/security/2021/02/death-of-emotet.html#ladybird) and get the username we should use!

> Operation: ladybird

Now all that's left to do is ssh in and grab the flag.
Note, you will need to change the permissions on the key in order to get it to work:
>chmod 600 p2.private.key

> ssh -i p2.private.key ladybird@0.cloud.chals.io -p 21986

![ask_and_recv_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ask_and_recv_2.png?raw=true)

## Ask and You Shall Recv 3

### This time, the flag is hosted on a webserver running internally at 0.cloud.chals.io on port 8888. SSH is exposed on port 27141. The private key for user tunneler is provided for download and the passphrase is cda-od.

### Can you figure out how to get to the flag?

#### Note - sharing private keys is always a bad idea - this is only for the purposes of the challenge.

For this one we need to follow the same steps as with the second challenge, only this time we need to forward port 8888 on the remote host to our local machine, we can then view the flag on a web browser at 
>127.0.0.1:8888.

> ssh -i p3.private.key -L 8888:localhost:8888 tunneler@0.cloud.chals.io -p 27141

![ask_and_recv_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ima.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/back_to_basics_1_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/signed_and_secured)