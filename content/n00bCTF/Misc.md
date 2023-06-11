---
title: "n00bCTF Misc challenges"
date: 2023-05-25T13:25:32-05:00
tags: ['n00bCTF','Writeups', 'Misc']
---
 
# [home](https://jjolley91.github.io/blog)

 # Intro
These are the solutions I was able to find under the Misc category.


### Sanity check

This one was pretty straightforward, the prompt reads:

```TXT
Welcome to n00bzCTF2023! Make sure to read the rules on our website.
```
```
 There might be something 😉Also don't forget to join our discord server at https://discord.com/invite/Kze7sjpgf7.
```

I simply went to the /rules page and viewed the page source. After scrolling you can find the flag! 
```
Flag: n00bz{w3lc0m3_t0_n00bzCTF_2023!}
```
![sanity](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/sanity.png?raw=true)



### Amazing Song Lyrics

Prompt: 

```
This is a wierd png file. I hope you can make some sense out of it!
```
There is a link to download chall.png

I downloaded the file and decided to check the strings:

```bash
strings chall
```

I found the flag!!

```
Flag: n00bz{N3v3R_$torE_$ENs1TIV3_1nFOrMa7IOn_P1aiNtexT_In_yoUr_bin4rI3S!!!!!}
```
![Amazing_song_lyrics](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/Amazing_song_lyrics.png?raw=true)



### My Chemical Romance

Prompt:

```
My friend loves Chemistry very much specially the elements.
```
```
Once I asked him the wifi password he gave me some numbers like 186808155710 and told me that the number are in group of two
 ```
 ```
like 1008 -> 10 and 08/8. Can you help to gather the wifi password? (Note: It forms a complete word, so you might have to leave out something).
```

we are given the code: 186808155710

we are told to group the numbers by twos, and since the challenge mentions chemistry I decided to see if the numbers matched atomic numbers on the perodic table, then used the element abbreviation as the key:

18 ar
68 er
08 o
15 p
57 la
10 ne
aeroplane

Then I wrapped the anwer in the flag{} format and solved the challenge!
```
Flag: n00bz{aeroplane}
```

