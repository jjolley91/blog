---
title: "Puzzle Pieces"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Hard','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/motw)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/crimson_initiate)

### I had a flag on this handy QR code, but a fiend cut it up into pieces and threw one of them away! Is there still a way to retrieve the flag?

This one is an interesting challenge, in my opinion. The trick is to assemble the three pieces, and then add the fourth piece which can be done by inserting the bottom left fragment and rotating it 90 degrees. 

This is possible because the qr code contains redundant data nested inside it. All we are really missing to extract the data is the position detection pattern in the top left. If you arent very precise with your reassembly you might need to also correct the timing, but after that the assembled qr can be uploaded to [QRazyBox](https://merri.cx/qrazybox/), and use the Tools > extract data to retrieve the flag!

![puzzle_pieces](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/puzzle_pieces.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/motw)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/crimson_initiate)