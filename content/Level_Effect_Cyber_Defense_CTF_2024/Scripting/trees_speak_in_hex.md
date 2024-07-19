---
title: "The trees speak hexadecimal"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Scripting','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Scripting](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Scripting/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Scripting/hay_in_a_needlestack)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/)

### As a result of their investigation, the Incident Response team has identified 10 malicious files and provided us the "bad" hashes in iocs.txt.

### They have also collected various file hashes across 20 different hosts on our network. These are stored in text files where each host has its own file containing 40 hashes, all bundled up in collections.zip. The bad hashes are likely present in some of the collections.

### Your objective is to identify the number of occurrences of each bad hash across the host collection files. The flag is the sum of the occurrences of all bad hashes.

#### Note: You have 3 attempts max to get the right number

Here we are given a collections.zip and an iocs.txt file to download. Unzipping the collections gives us a directory with several text files, each containing a bunch of hashes we need to sort through. you COULD do this manually, but I wouldnt recommend it. Instead we can whip up a simple python script to do the job for us:

```py
import os

def read_hashes(filename):
    hashes = set()
    with open(filename, 'r') as file:
        for line in file:
            line = line.strip()
            if line: 
                hashes.add(line)
    return hashes
def count_hashes(filepath, hash_set):
    count = 0
    with open(filepath, 'r') as file:
        for line in file:
            line = line.strip()
            if line in hash_set:
                count += 1
    return count
def count_total_hashes(directory, hash_set):
    total_count = 0
    for dirpath, _, filenames in os.walk(directory):
        for filename in filenames:
            if filename.endswith('.txt'):
                file_path = os.path.join(dirpath, filename)
                total_count += count_hashes(file_path, hash_set)
    return total_count
iocs_file = 'iocs.txt'
directory_path = 'collections/'
hashes_set = read_hashes(iocs_file)
total_hashes_count = count_total_hashes(directory_path, hashes_set)
print(f"Total number of hashes found in the files: {total_hashes_count}")
```
![hex](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/hex.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Scripting/hay_in_a_needlestack)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/)