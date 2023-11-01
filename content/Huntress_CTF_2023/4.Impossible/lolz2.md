---
title: "lolz#2"
date: -
#draft: true
tags: ['CTF', 'Writeups', 'Impossible Difficulty', 'Extreme']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Impossible Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/3.Hard/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/4.Impossible)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/4.Impossible/lolz3) 

* Please note that this challenge was a community effort and much of the content in this writeup is attributed to findings from the public discourse.

### 籖ꍨ穉鵨杤𒅆象𓍆穉鵨詌ꍸ穌橊救硖穤歊晑硒敤睊ꉑ硊ꉤ晊ꉑ硆詤橆赑硤ꉑ穊赑硤詥楊ꉑ睖ꉥ橊赑睤ꉥ杊𐙑硬ꉒ橆𐙑硨穒祊ꉑ硖詤桊赑硤詥晊晑牙

The provided string is reminiscent of the previous challenge BaseFFFF+1, suggesting that it is base65536 encoded.
We used [this site](https://www.better-converter.com/Encoders-Decoders/Base65536-Decode) to decode it and reveal a base64 encoded string which itself decoded to:

```txt
The Hawaiian Ha-Le,ByCEBtBzCTBwBABBBvBuBABuAyAwBBBDAwByBxBEAzByAwAzBvByBFAyBxBDBCBEBuBwAwByBuCV
```

We weren't too sure about "The Hawaiian Ha-Le", but we knew the following portion was encoded in some way. It wasn't an encoding we could easily identify.

Eventually, we noticed that the string length is twice the length of the standard flag (38 characters). This indicated that every 2-character group in the encoded string corresponds to a character in the flag.

So, we started with 'flag' and '{}' to map the following:
```txt
By -> f
CE -> l
Bt -> a
Bz -> g
CT -> {
CV -> }
```

We could see that the encoded text corresponds to 0-9 + a-z + special characters. Using what we knew, we ordered all the encoded character groups alphabetically to produce the following:
```txt
Aw ->
Ay ->
Az ->
BA ->
BB ->
BC ->
BD ->
BE ->
BF ->
Bt -> a
Bu ->
Bv ->
Bw ->
Bx ->
By -> f
Bz -> g
CE -> l
CT -> {
CV -> }
```

At this point, we just filled in the rest while following the pattern:
```txt
Aw -> 0
Ay -> 2
Az -> 3
BA -> 4
BB -> 5
BC -> 6
BD -> 7
BE -> 8
BF -> 9
Bt -> a
Bu -> b
Bv -> c
Bw -> d
Bx -> e
By -> f
Bz -> g
CE -> l
CT -> {
CV -> }
```

With all the characters mapped, we can get the flag!
```txt
By CE Bt Bz CT Bw BA BB Bv Bu BA Bu Ay Aw BB BD Aw By Bx BE Az By Aw Az Bv By BF Ay Bx BD BC BE Bu Bw Aw By Bu CV
 f  l  a  g  {  d  4  5  c  b  4  b  2  0  5  7  0  f  e  8  3  f  0  3  c  f  9  2  e  7  6  8  b  d  0  f  b  }
```

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/4.Impossible)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/4.Impossible/lolz3) 