---
title: "MoTW"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/haystack)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/puzzle_pieces)

#### NOTE - The resources needed for this challenge are on the Cyber Defense CTF Triage Workstation VM on our hosted platform.

### Find out where the file forest_stream.jpg was downloaded from on the Triage Workstation and you'll have your flag!

For this challenge, we are directed to the Cyber Defense CTF Triage Workstation hosted vm.

We can try to look at some data in the photo, but this does not result in anything useful. Instead, we can use the Zone.Identifier alternate data stream if we open a powershell window in the Downloads folder:

```powershell
Get-Content -Path ".\forest_stream.jpg" -Stream Zone.Identifier
````
All that's left to do is url decode and submit the flag!

![motw](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/motw.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/haystack)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/puzzle_pieces) 