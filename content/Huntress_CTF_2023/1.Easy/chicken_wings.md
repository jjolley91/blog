---
title: "Chicken Wings"
date: 2023-10-09T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dumpster_fire)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/wimble) 

### I ordered chicken wings at the local restaurant, but uh... this really isn't what I was expecting... 

Here we are given a file 'chicken_wings' to download.

Running the 'file' command reveals that it is a text file. If we cat the file, we are given a wierd set of characters. 
```
♐●♋♑❀♏📁🖮🖲📂♍♏⌛🖰♐🖮📂🖰📂🖰🖰♍📁🗏🖮🖰♌📂♍📁♋🗏♌♎♍🖲♏❝
```

If we take the challenge name as a hint (and it is) we can reason that this might be the font wingdings. There is a helpful online tool [here](https://www.dcode.fr/wingdings-font)(dcode.fr)that will immedately decode the funky font and give us the flag!

![wings](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/wings.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dumpster_fire)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/wimble) 