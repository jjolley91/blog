---
title: "How many donuts?"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Scripting','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Scripting](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/perfect_match)

### Samwise, I've had enough of your lembas bread. I want donuts. How many you ask? well I wrote you a script. It mostly works, but the answer will be revealed when it does. I mean at least a couple of them!

For this challenge, we are given a bash script to download: HowManyDonuts.sh, which contains several errors. The objective is to fix these errors and retrieve the flag.

I will go through the changes needed step by step.
Original script:
```bash
#!/bin/bash

# You wanted to know how many donuts I wanted? I wrote a script for you that will provide you the answer. Pretty sure it works - I think.

# Define the list of ASCII values
ascii_values=(102 104 116 122 117 113 106 116 107 103 116 125 106 115)

# Function to convert ASCII values to characters and print them as a word
print_word_from_ascii() {
    local word=""
    for value in "${ascii_values[@]}"; do
        char=$(printf "\\$(printf "$value")")
        word+="$char"
        word+="$char"
    done
    echo "$word"
}

# Loop to print the word 5 times, decreasing ASCII values each time
for i in {1..3}; do
    print_word_from_ascii "${ascii_values[@]}"
    # Decrease each ASCII value by 1
    for j in "${!ascii_values[@]}"; do
        ascii_values[j]=$((ascii_values[j]-11))
    done
done
```
Luckily this was a GOOD developer, and they put comments in the script to describe the intended functions. We can inspect the script and see why it isnt running.

1. for the print_word_from_ascii function we can see that they are trying to print each character from the ascii values, however, they are trying to print each character twice. Therefore, we can remove the second one.
```bash
print_word_from_ascii() {
    local word=""
    for value in "${ascii_values[@]}"; do
        char=$(printf "\\$(printf "$value")")
        word+="$char"
    done
    echo "$word"
}
```

2. Next we can see a comment about printing the word 5 times, however the loop only does this 3 times. We can correct that here:
```bash
for i in {1..5}; do
```

3. In the same comment they mention decreasing the ascii values each time, and later we see they should be decreasing by 1. However the current script is decreasing them by 11. We can correct that next.

```bash 
    print_word_from_ascii "${ascii_values[@]}"
    # Decrease each ASCII value by 1
    for j in "${!ascii_values[@]}"; do
        ascii_values[j]=$((ascii_values[j]-1))
    done
done
```
3. The script still isnt printing correctly at this point. If we look carefully we can understand that the printf "$value" is not the correct way to convert ascii values to characters using printf. Instead, we need to change it to:
```bash
char=$(printf "\\$(printf "%o" "$value")")
```
4. We need to make the script executable on our linux system:
```bash
chmod +x HowManyDonuts.sh
```
Finally we get the output:
```bash
./HowManyDonuts.sh
fhtzuqjtkgt}js
egsytpisjfs|ir
dfrxsohrier{hq
ceqwrngqhdqzgp
bdpvqmfpgcpyfo
```
We can put it through a rot cypher and adjust the amount to either 24, or -2 and retrieve the flag.

![donuts](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/donuts.png?raw=true)

To make the script print the flag directly, we can modify it like so:

```bash
print_word_from_ascii() {
    local word=""
    for value in "${ascii_values[@]}"; do
        char=$(printf "\\$(printf "%o" "$(( (value - 97 + 25) % 26 + 97 ))")")
        word+="$char"
    done
    echo "$word"
}

# Loop to print the word 5 times, decreasing ASCII values each time
for i in {1..5}; do
    # Decrease each ASCII value by 1
    for j in "${!ascii_values[@]}"; do
        ascii_values[j]=$((ascii_values[j]-1))
    done
    # Check if it's the 4th line (index 3 since arrays are zero-indexed)
    if [ $i -eq 4 ]; then
        print_word_from_ascii "${ascii_values[@]}"
    fi
done

```


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/scripting/perfect_match)