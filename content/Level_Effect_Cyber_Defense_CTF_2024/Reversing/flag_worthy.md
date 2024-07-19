---
title: "Think you're flag worthy?"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Reversing','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Reversing](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/cradle_1_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/shortcut)

### The flag may be encrypted but it most certainly can be recovered. Can you retrieve it?

### There are a few ways to approach this one, some more efficient than others.

```ps
$key = "seinfeld"; -join ([char[]](([Text.Encoding]::UTF8.GetString(([Convert]::FromBase64String("GgNJRkdFNxcHFwAAAThWXjoWJxsKCSMWNggZGh9NNzcKFh0LC0spCgUMGwEICAkKBzhTVCEAGCEdEwAcCQsBAR0RPw8UDA0GHwBBSTYpKSUgIE5HT0xMH3lFSU5GQQoIEgJJU0ZHAAEFAAULAAMJBwceGgsUAAINBxw2AAkSEUZ5RUlORjIeDQcARCETERwRB0VLLwUGCRcARQ4cBwsYARdJSRoOAEwCHwQOTg8WVkRXAwUPAUdmGVMABR0DRRduU0VJTjEXBRAWSCYbEhUZEFNHKAZKRQ0MX0UIBkdFNQsGRQ0HAgtLEFMWCBdGEQQBUwgICQ8GTBMcFw1PRG8R") | % { [char]($_ -bxor [byte][char]$key[$i++ % $key.Length]) } -begin { $i=0 }))))) | iex
```

Here, we are given another powershell script which has been obfuscated. If we paste everything up to and excluding the '| iex' we find that we get an output: "Ah, ah, ah! You didn't say the magic word!"

However, if we look at the text above, we can see that it still prints the flag... well, okay then! 


![flag_worthy](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/flag_worthy.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/cradle_1_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/reversing/shortcut)