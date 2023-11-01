---
title: "Rock, Paper, Psychic"
date: 2023-10-15T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/tragedy)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/rogue_inbox) 

### Wanna play a game of rock, paper, scissors against a computer that can read your mind? Sounds fun, right? 

Here we are given a compiled binary to download 'rock_paper_psychic.exe' if we run the program in a windows vm we find that we can play a game of rock paper scissors in the commandline, however the computer always wins.

![rock_paper](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rock_paper1.png?raw=true)


We decided to try analyzing this using Ghidra to see if we could find a way to trigger a win condition.

Upon analyzing the functions and strings a few stood out as noteworthy:

```assembly
printFlag_main_6 function playerWins_main_10, determineWinner_main_58
```
When we inspected the printFlag function, we found a variable 'fromRC4__OOZOnimbleZpkgsZ8267524548O49O48Z826752_75' which indicated that the flag might be encrypted using RC4. RC4 stands for "Rivest Cipher 4". It's a variable key-size stream cipher, meaning it can use keys of varying lengths, commonly ranging from 40 to 256 bits. RC4 is known for its simplicity and speed.

When viewing the function in the assembly side, we noticed a long string being written one character at a time:
```text
@D1E2A0D9FA89CABED207EDF4F55C688E04EBE20F077351BDAA1E110D5A74805C916AF12F054C
```
As well as what appeared to be a key to decrypt:
```text
gnnhexnyjkwpaghynzfthadollhtrhballsdmhhnbjppewgjkhnlhspwjswqoxtgdykxrhwlabblekxj
```

![rock_paper2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rock_paper2.png?raw=true)


We decided to paste these values into [dcode](https://www.dcode.fr/rc4-cipher)'s RC4 decryptor, and were able to retrieve the flag!

![rock_paper3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rock_paper3.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/tragedy)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/rogue_inbox) 


