---
title: "Zig Challenges (IR and Reversing)"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Incident_Response','Reversing','Easy','Medium','Hard','Binary_Triage']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) 


#### All of the Zig challenges are designed in such a way that actually triaging the infected workstation will naturally lead you to the required flags. All of these challenges were solved on the Cyber Defense CTF Triage Workstation

## #1: What you say!? (Easy)

### This response would have bought you a little more time!

For this challenge, we simply need to run the Zig.exe on the workstation, and try the responses until we find that one response gives us extra time before the reboot. This is option 2 and is the same option as the name of the challenge. I will also note that entering anything other than the 4 pre-programmed responses causes the program to exit immediately.

![what_you_say](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/what_you_say.png?raw=true)


## #2 Gimme _____ Checks Towards the Door! (Easy)

### _____Checks started this all.

For the next answer, we can run the zig.exe and notice that the program does 3 systems checks before presenting the options. This gives us our answer: 3.

![checks_toward_the_door](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/checks_toward_the_door.png?raw=true)


## #3 Save zig move zig (Easy)

### I am the name that called the zig mover.

This challenge is where the binary triage really begins. After the zig.exe response causes the vm to reboot, you might notice a few powershell windows flash across the screen. This could indicate some persistence was installed on the machine, so we should start the investigation by looking for anything of that nature using Autoruns.

We can quickly find an HKCU Registry run key named "MyApp" which is pointing to a rundlll32.exe binary in the C:\Windows directory. This is an attempt at masquerading, as the legitimate windows binary should be rundll32.exe. We can proceed to the directory and dump the strings on this to continue the investigation.

![my_app](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/my_app.png?raw=true)

Dump strings:

```powershell
strings.exe .\rundlll32.exe > rundlll_strings.txt
```

After inspecting the strings we find a reference to C:\Windows\base.out which, when inspected, appears to be the output of a keylogger which is recording each user keystroke.

![base_out](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/base_out.png?raw=true)

There is not much else helpful in the strings of the rundlll binary for now, so we can turn our attention back to autoruns and look to see if there is anything else we might have missed. After a closer inspection, we find a scheduled task named "ScreenSaver", which is running Windows powershell and calling a script "C:\ProgramData\movezig.ps1"

This gives us the the flag for the challenge, as the name which is calling the zig mover is: 'ScreenSaver'.


![screen_saver](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/screen_saver.png?raw=true)


## #4 Keylogger Out #1 (Medium)

### What was the file name for the first key logger output?

We have already stumbled across the answer to this question during the earlier triage. 

To summerize: We found a registry run key which was pointing to rundlll32.exe in the C:\Windows directory. Dumping and reading the strings of that binary revealed a file in the same directory named base.out, which ended up being a keylogger output as noted above. 

Thus the answer to this challenge: base.out

## #5 One Of These Process Names Is Not Like The Other (Medium)

### I am the logger.

Again, we have already found the answer to this with our normal triage of the system: rundlll32.exe


## #6 Whose App Was It Anyway? (Medium)

### I ran the logger after I mislead you from the first console screen.

The answer to this is the name of the registry run key that is calling the rundlll32.exe binary: MyApp

## #7 Your Base, My Base (Medium)

### I took your keys to this domain.

To answer this question, we can continue our investigation and analyze the movezig.ps1 script which was being pointed to by the ScreenSaver scheduled task.

Opening this script in notepad++ we see the script is trying to execute a PUT request of the base.out file to: leveleffectgotallyourbaase.com

![your_base_my_base](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/your_base_my_base.png?raw=true)


## #8 Where Did I Come From? (Hard)

### I must have come from somewhere originally. (provide the full URL please) ("I" is not Zig.exe but rather what it calls)


For this challenge, we need to go back to the original zig.exe binary. We can try dumping the strings. After inspecting the strings of the binary, we find reference to a url to download the rundlll32.exe binary. Thus we have the answer to this question:
```
https[:]//cda-lab-data.s3.amazonaws.com/FAQingFriday/rundlll32.exe
```

![where_did_i_come_from](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/where_did_i_come_from.png?raw=true)




## #9 Key Logger #2 (Hard)

### I was a bit trickier to find! What was my file name?


For this challenge, we again, can go back and inspect the strings dumped from the rundlll32.exe binary. If we look for more .out files, we find a file in a different directory: C:\Program Files\WindowsPowerShell\misdirection.out

![logger_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/logger_2.png?raw=true)

Sure enough, if we inspect the misdirection.out, it is a second keylogger output file.

Thus the answer to this question: misdirection.out


# The final two Zig challenges are from the Reversing category of the CTF.

## #10 I Have Called for Help (Hard)

### What secret set of keys could have been initiated for help?


For this challenge, we need to do some reversing. I used [Ghidra](https://ghidra-sre.org/) for this. From the strings of the binaries, we will note that they were written in GoLang. GoLang is particularly difficult to reverse given the huge file size of the compiled binaries. This is due to the fact that the libaries are statically linked, this results in no dependency issues for the compiled binaries.
However, to reduce the file size most developers will also remove the function names and debugging symbols. This results in thousands of functions when decompiled in Ghidra, and finding anything useful can be a nightmare. Luckily, we can import a few scripts into Ghidra that are specifically designed to make the process a bit easier from [Here](https://github.com/getCUJO/ThreatIntel).

I spent a lot of time with the Zig.exe binary only to come up empty handed. I then remembered we had another binary that could be inspected: rundlll32.exe. Decompiling the main.main function shows that it calls a function main.main.func1, The answer to our question can be found there, as it listens for keyboard inputs and takes an action if they are equal to the string: helpmeobiwan. 

![help_me](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/help_me.png?raw=true)



## #11 My Lament (Hard)

### I would have screamed this had I exited in such a way. (first 6 characters is fine!)

I will be honest, I solved this one by actually lamenting at this challenge.

However, we can find a reference to it in the strings of the rundlll32.exe binary.

![lament](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/lament.png?raw=true)


Flag: noooooo


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/)