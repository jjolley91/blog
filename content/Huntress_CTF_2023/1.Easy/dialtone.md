---
title: "Dialtone"
date: 2023-10-06T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/i_wont_let_you_down)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/php_stager) 

### Well would you listen to those notes, that must be some long phone number or something! 

Here we are given a 'dialtone.wav' file to download. This is an audio file, and listening to it sounds like someone is dialing a phone number. 

We can use an online [DTMF decoder](https://dtmf.netlify.app/) this one worked nicely for us. The result is a long string of numbers.
```txt
13040004482820197714705083053746380382743933853520408575731743622366387462228661894777288573
```

Here's some JS code that takes the decoded DTMF (bigint), converts it to hex, then decodes the hex to the flag:

```js 
var hex = 13040004482820197714705083053746380382743933853520408575731743622366387462228661894777288573n.toString(16);var str = '';for (var n = 0; n < hex.length; n += 2) {str += String.fromCharCode(parseInt(hex.substr(n, 2), 16))}console.log(str);
```
We were able to decode this into the flag using this [site](https://scwf.dima.ninja/)

![dialtone](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/dialtone.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/i_wont_let_you_down)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/php_stager) 