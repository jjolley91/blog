---
title: "Perfect Match"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Scripting','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Scripting](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/how_many_donuts)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/hay_in_a_needlestack)

### Regex - love it or hate it, it's an invaluable skill to have as a defender.

### The goal of this challenge is to extract all IPv4 addresses from the contents of the file input.txt . A starter script has been provided below and by download. All you need to do is insert a regex pattern to finish the job. You can submit your code in the code submission box.

#### Note: If you write your own script, you must read in the data from input.txt specifically as shown in the example.

### Starter script:
```python
import re

PATTERN = re.compile(r'YOUR PATTERN HERE')

def extract_ips(data):
    ips = PATTERN.findall(data)

    unique_ips = []
    [unique_ips.append(str(ip)) for ip in ips if ip not in unique_ips]

    return unique_ips

def main():
    with open("input.txt") as f:
        data = f.read()
        extracted_ips = extract_ips(data)

    for ip in extracted_ips:
        print(ip)

main()
```

For this challenge, we are given an extract.py script, and an input.txt to download and work with.

If we inspect the input.txt file we see that it is an assortment of log dumps we need to sift through. The extract.py file is the same as given above. We need to come up with some regex pattern to extract all of the ipv4 addresses from the log.

This regex does the trick:

```py
(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)
```
We can paste it into the submission script and complete the challenge. 


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/how_many_donuts)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/hay_in_a_needlestack)