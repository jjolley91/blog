---
title: "JuiceShop vs cryptography"
date: 2023-05-25T13:25:32-05:00
tags: ['JuiceShop','Writeups','Cryptography']
---


In this writeup I will be exploring the cryptographic challenges within OWASP Juice Shop.


Confidential Document

While trying to read the confidential document we come across this /ftp directory, which we will visit for the next section.

![finding_ftp](https://github.com/jjolley91/blog/blob/main/static/cryptography/finding_ftp.png?raw=true)



### Nested Easter Egg
#### Difficulty: Moderate

From the /ftp directory there is an interesting document titled 'eastere.gg'. I tried to click on this, but received an error stating that only .md and .pdf files are allowed.  

we can add a URL encoded null byte in the address bar and then append the .md to make the server think we are asking for one of the valid file types.


![downloading_easteregg](https://github.com/jjolley91/blog/blob/main/static/cryptography/downloading_easteregg.png?raw=true)


I opened the file in notepad++ and found the next step in the puzzle:


[viewing_easteregg](https://github.com/jjolley91/blog/blob/main/static/cryptography/viewing_easteregg.png?raw=true)


The string "L2d1ci9xcmlmL25lci9mYi9zaGFhbC9ndXJsL3V2cS9uYS9ybmZncmUvcnR0L2p2Z3V2YS9ndXIvcm5mZ3JlL3J0dA=="

The fact that this ends in a double equal indicates that this is base64 encoded.

I plugged this into cyberchef, and the output looks like a directory path, but not a human readable one...

![decrypt_stage_1](https://github.com/jjolley91/blog/blob/main/static/cryptography/decrypt_stage_1.png?raw=true)


After trying some different decoding methods, I found that Rot13 cypher returned something that looks like a valid path.

![decrypt_stage_2](https://github.com/jjolley91/blog/blob/main/static/cryptography/decrypt_stage_2.png?raw=true)


Finally I went back to juice shop and pasted in this path and found a strange planet. 

After tweaking the settings on the page I was able to see the symbol on the planet seems to be some sort of plant!

![easteregg_solution](https://github.com/jjolley91/blog/blob/main/static/cryptography/easteregg_solution.png?raw=true)

Returning to the score board I found that the challenge was now solved.




