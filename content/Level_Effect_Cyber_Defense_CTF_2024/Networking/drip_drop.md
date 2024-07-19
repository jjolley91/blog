---
title: "Drip Drop"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Networking','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Networking](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/et_tu_brute)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/)

### A host on the network was compromised and the threat actor was likely able to exfiltrate sensitive information. They did well to hide their tracks on the endpoint, but fortunately we have a traffic capture from around the time of intrusion. Can you determine if any data was stolen?

#### AKA "The Final Boss"

For this challenge, we are given xfil.pcap to download and inspect. Upon initial inspection it seems like we have a lot of http traffic which is mostly GET requests to various directories on the webserver, and we can tell by the user-agent string that this was being automated with python. There is also a post request which stands out with the string "You'll probably need these". The post request is to /login and there are some interesting strings in the username and password fields:
> {"username": "3e1d1f4c8a7b456a9f4d5b3f2c6e8a1d", "password": "5b8e2a27dc43bc967c435a7c8c3ab0fc5294b4c0a27c68719a621f0348be5c1a"}
![drip_drop_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/drip_drop_1.png?raw=true)

This looks like an AES decryption key, and an IV, so we can put that aside for later until we can find the paylodad to decrypt.

The next step is to pull out 20-30% of your hair looking for the payload. There was nothing else interesting in the http traffic which leaves us with the only remaining traffic: ICMP. 

The data in all of the ICMP packets is the same, and cannot be decrypted using the found keys, so this is a dead end. Looking around for anything which is unique between packets we can eventually see that the only thing which seems to stand out as unique to each packet is the time...

![drip_drop_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/drip_drop_2.png?raw=true)

There does seem to be a pattern here to investigate.
Note: I had my time set to seconds since last displayed packet.

Each of the time values has a difference of 0-1.5 seconds. This seems like it might be binary in some way. However, pulling out these time values was not leading to anything useful...

Since this is data Exfiltration, we can try looking at it through the lense of only the icmp REQUEST packets.

> icmp.type==8

After applying that filter the time delta looks a lot more like usable binary.
![drip_drop_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/drip_drop_3.png?raw=true)

We can begin extracting the values to proceed using tshark:

> tshark -r exfil.pcap -Y "icmp.type==8" -T fields -e frame.time > raw_time.txt

> awk '{split($4, t, ":"); printf "%.2f\n", t[3]}' raw_time.txt > time_delta.txt

After runng these commands to clean up the data a little bit we get:

![drip_drop_4](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/drip_drop_4.png?raw=true)

We know the time difference between packets is ~0.5-1.5 seconds, so we can use a python script to subtract each pair of values, and append the difference to a file to check:

```python
with open('time_delta.txt', 'r') as f:
    values = f.readlines()
values = [float(value.strip()) for value in values]
wrap_threshold = 60.0
differences = []
for i in range(len(values) - 1):
    diff = values[i+1] - values[i]
    if diff < 0: 
        diff += wrap_threshold
    differences.append(int(diff))
with open('binary.txt', 'w') as f:
    f.write(''.join(map(str, differences)))
 ```

Finally! The resulting binary actually decodes to valid hex!

```011000110110010101100101001101100011001100110000011001010011000001100
011011000010011001101100101001100010011001001100100011000010011011001100
101001100000110001100111001001101000011001100110000001101000011001000110
010001100010110001100110111011001010110001100110110001100010011011100110
010001100100110010001100101001100010011011000110111011000110011001101100
010001101000110010100110001001101100011001000111000001101010011011001100
011011000100011100100110001001100010110001101100110001101100110010001100
011001101100011001100110010001100110011000100110100001100110011010101100
001001100010011001001100011001101110011001100110011001101010011001001100
010011001100110000100111000001101100110010100110110001110000011011000110
110001100010011010100110111001100110110000101100010
```
> cee630e0ca3e12da6e0c94304221c7ec61722de167c3b4e162856cb911cf6dc63231435a12c73352bfa86e68661573ab

At long last, we can use our keys for decryption and retrieve the flag!

![drip_drop_final](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/drip_drop_final.png?raw=true)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/networking/et_tu_brute)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/crypto/)

