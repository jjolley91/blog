---
title: "Cipher Pudding"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Cryptography','Medium','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Crypto](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/pasta_filiformis)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/bits_abound)

### Wings for dessert? But it's good to the last byte.
```
❄︎●︎☼︎☼︎☪︎📁︎📂︎🕆︎☼︎✠︎●︎☺︎☼︎☜︎📂︎🗄︎💧︎🕆︎☼︎✞︎💣︎☜︎●︎☜︎✞︎✠︎◻︎☺︎☼︎☜︎📂︎🗄︎💧︎🕆︎☼︎✞︎💣︎🕆︎●︎☜︎✞︎❄︎👌︎☺︎☼︎☜︎📂︎🗄︎💧︎🕆︎☼︎✞︎💣︎☜︎●︎☜︎✞︎✠︎◻︎☺︎☼︎☜︎📂︎🗄︎💧︎🕆︎☼︎✞︎💣︎☜︎●︎☜︎☼︎✠︎♒︎☠︎♋︎🕆︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎👎︎✈︎❄︎☞︎☠︎♏︎🕆︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎👎︎✈︎❄︎☞︎⚐︎✈︎📁︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎👎︎✈︎❄︎☞︎⚐︎✈︎📁︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎👎︎✈︎❄︎☞︎☠︎♏︎🕆︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎👎︎✈︎❄︎☞︎☠︎🕆︎📁︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎❄︎✈︎❄︎☞︎☠︎♋︎🕆︎☞︎⌛︎❄︎🕈︎●︎👌︎💣︎🕆︎🗄︎❄︎✈︎✠︎♒︎☠︎✞︎☜︎✞︎■︎❄︎✠︎◻︎☺︎☪︎📁︎🗄︎🕆︎🕆︎🕈︎♎︎⚐︎✞︎☞︎●︎■︎❄︎✠︎◻︎☺︎☪︎📁︎🗄︎🕆︎☼︎🕈︎♎︎⚐︎✞︎☜︎●︎■︎❄︎✠︎◻︎☺︎☪︎📁︎🗄︎🕆︎🕆︎🕈︎♎︎⚐︎✞︎☝︎☠︎■︎❄︎✠︎◻︎☺︎☪︎📁︎🗄︎🕆︎☼︎🕈︎♎︎⚐︎☼︎☝︎⧫︎■︎❄︎✠︎◻︎☺︎☪︎📁︎🗄︎🕆︎❄︎🕈︎♎︎☠︎✞︎☜︎🕆︎⌧︎💧︎🕆︎☼︎☠︎♏︎🕆︎●︎☜︎✞︎✠︎♒︎☺︎☼︎☞︎🕆︎⌧︎💧︎🕆︎☼︎☠︎♏︎🕆︎●︎☜︎✞︎✠︎♒︎☺︎☼︎☞︎☜︎📁︎💧︎🕆︎☼︎☠︎♏︎🕆︎●︎☜︎✞︎✠︎◻︎☺︎☼︎☜︎✞︎🗐︎❄︎●︎☠︎👌︎♏︎🙵📂︎◻︎✈︎❄︎☞︎☠︎🕆︎📁︎☜︎⌧︎❄︎●︎☠︎👌︎♏︎🙵📂︎◻︎✈︎❄︎☞︎⚐︎✈︎📁︎☜︎⌧︎❄︎❍︎●︎👌︎♏︎🙵📂︎◻︎✈︎❄︎☞︎☠︎🕆︎📁︎☜︎⌧︎❄︎✞︎☠︎👌︎♏︎🙵📂︎◻︎✈︎❄︎☞︎☠︎♏︎🕆︎☞︎🗐︎❄︎✞︎☼︎✞︎☪︎📁︎📂︎⌛︎💧︎🕈︎♎︎⚐︎✞︎☞︎☞︎■︎❄︎●︎☼︎☞︎☪︎📁︎📂︎⌛︎💧︎🕈︎♎︎⚐︎✞︎☞︎☞︎■︎❄︎●︎☼︎☪︎☪︎📁︎📂︎⌛︎💧︎🕈︎♎︎⚐︎✞︎☜︎✞︎■︎❄︎●︎☼︎☞︎☪︎📁︎📂︎⌛︎💧︎🕈︎♎︎⚐︎✞︎☞︎☞︎■︎❄︎●︎☼︎☼︎☪︎📁︎📂︎⌛︎💧︎🕈︎♎︎⚐︎✞︎☞︎✞︎■︎❄︎✞︎☼︎☞︎♏︎♑︎🖬︎🖬︎
```

On to the last course! Here we are given another encoded message. These symbols are in a font called 'Wingdings', as the hint in the prompt suggests. The first step can be decoded using a [wingdings decoder](https://lingojam.com/WingdingsTranslator) such as this one:

![cipher_pudding_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/cipher_pudding_1.png?raw=true)

The rest can be decoded in [Cyberchef](https://cyberchef.org/) using the following steps:
* from base64 
* from base64 
* from decimal 
* rot13 
* from hex


![cipher_pudding_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/cipher_pudding_2.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/pasta_filiformis)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/bits_abound)