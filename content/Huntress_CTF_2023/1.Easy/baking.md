---
title: "Baking"
date: 2023-10-11T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/f12)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/vbe) 

### Do you know how to make cookies? How about HTTP flavored? 

Here we are able to spin up a web server which brings us to a page from which we are able to select a recipe to 'bake'. From the list, Magic Cookies look like the thing we're after, but they take a while to finish (120 hours)!!

![baking_1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/baking_1.png?raw=true)


If we take the name of the challenge as a hint, we can start them baking, and use the DevTools to check if we have any session cookies set.

Sure enough, we have a cookie named in_oven, with a value that seems to be base64 encoded.

![baking_2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/baking_2.png?raw=true)


If we decode the cookie value, we get the following output: 
```bash
echo "eyJyZWNpcGUiOiAiTWFnaWMgQ29va2llcyIsICJ0aW1lIjogIjEwLzE2LzIwMjMsIDIxOjEzOjEyIn0=" | base64 -d
```
```bash
{"recipe": "Magic Cookies", "time": "10/16/2023, 21:13:12"}  
```

We decided to try changing the time to T-7200 minutes,

```bash
echo '{"recipe": "Magic Cookies", "time": "01/01/2001, 21:13:12"}' | base64  
```
and change the value of the cookie to the result, then refresh the page. Sure enough, we got the flag!!! And some admittedly stale cookies...


![baking_3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/baking_3.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/f12)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/vbe) 