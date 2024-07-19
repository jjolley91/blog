---
title: "Bits Abound"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Cryptography','Medium','Steganography']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Crypto](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/cipher_pudding)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/rock_on)

### I have a key with a curious code etched into it but not a clue where it goes. Here, take a look and let me know if you discover anything even the least bit significant about it.

For this challenge, we are given a key.png to download.

![key](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/key.png?raw=true)

The trick here is to extract the least significant bit from the image:
```python
from PIL import Image
import binascii
im = Image.open('key.png')
pix_val = list(im.getdata())
lsbs=""
for idx,val in enumerate(pix_val):
	lsbs=lsbs+'{0:08b}'.format(val[0])[-1]  
	lsbs=lsbs+'{0:08b}'.format(val[1])[-1]
	lsbs=lsbs+'{0:08b}'.format(val[2])[-1]
n=int(lsbs,2)
print(binascii.unhexlify('%x' % n))
```
The result gives us a long string of output, but if we look at the very beginning we see some unusual strings: 
> TW9Xb01vR2xEaVVxVmtYVVVlfnpUfn5+VmV+a09ufn5WZX5+Tm1EfklvU3c=

This looks like base64, and it does seem to decode, but not into a flag. We are still missing the final step, If we look back at the original image we see '21A' is printed on the key. All we need to do is XOR decrypt the remaining string to get the correct flag:

![bits_abound](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/bits_abound.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/cipher_pudding)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Crypto/rock_on)