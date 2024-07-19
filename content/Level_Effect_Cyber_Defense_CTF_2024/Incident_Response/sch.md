---
title: "SCH 1-10"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','incident_response','Easy','Medium','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [incident_response](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/autoruns_1_5)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/)


#### README - The resources needed for this challenge are on the Super Compromised Host (SCH) VM on our [hosted platform](https://training.leveleffect.com/courses/2a4dccb7-3d5b-4312-816e-ef3728d25b67). Use the VM on the Phase 2 CTF module if you've run out of hours on the original module.


## SCH Part 1 - A new challenger arrives (Easy)

### There is a suspicious user on the host with a password set to never expire. What is the username?

For this challenge, we can simply look for users who have their password set to never expire using powershell

```ps
wmic useraccount where "PasswordExpires=False" get Name
```

![sch_part_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_1.png?raw=true)


## SCH Part 2 - Part of the club (Easy)

### The suspicious user is a member of the local ______ group.

We can guess that the group they are talking about here is Administrators, and check it in powershell to verify:

```ps
net localgroup Administrators
```

![sch_part_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_2.png?raw=true)



## SCH Part 3 - Punctual process (Medium)

### The suspicious user registered something that executes every 5 minutes. What is the name given to it?

Something registered that runs every 5 minutes...sounds like a scheduled task. We can check Autoruns, and sure enough, something here stands out as strange:

![sch_part_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_3.png?raw=true)


## SCH Part 4 - Check in (Medium)

### I am executing enumeration commands every minute. What's my name?

For this, we can check Process Explorer, and quickly we will see a process is running which has a parent process of explorer.exe, which we did not start:


![sch_part_4](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_4.png?raw=true)

## SCH Part 5 - Pásale (Medium)

### I spawn 3 different processes. What are they?

#### The flag will be all three process names in alphabetical order, separated by colon without space, and SHA-256 hashed. Example:

> alpha.exe:bravo.exe:charlie.exe -> b9a6deb6189e70a01f92cd62fcb74ace7d2bbfb060205a18b2e936ae3cecd3c5


For this, we can note down the process id of olgreg.exe and open up Procmon. We can apply a filter:

> parent PID is #olgregpid
and
> Operation is Process Create

Since this is spawning the processes every minute, we dont need to wait long. We can quickly see that it is spawning the processes:

![sch_part_5](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_5.png?raw=true)

We can then simply put them in the format requested, and submit the sha256 hash as the answer:

```bash
echo -n "ipconfig.exe:net.exe:systeminfo.exe" | sha256sum
```


## SCH Part 6 - Check out (Medium)

### I am sending my precious enumeration data somewhere.

#### Provide the full domain and port, such as domain.tld:4444

For this challenge, we can return to the olgreg.exe process running in Process Explorer. We can right click on the process, click properties, and view the TCP/IP tab to find the domain with the connection ESTABLISHED, and submit the answer:

![sch_part_6](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_6.png?raw=true)

## SCH Part 7 - Wrong path (Medium)

### One of these services is not like the others. Which is it?

For this next part, we can return to Autoruns, and inspect the Services running on the machine. If we inspect one of the (Not Verified) services, we can see that it is running a file from the C:\Windows\Temp directory, which is unusual:

![sch_part_7](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_7.png?raw=true)

The name of the service is the answer.

## SCH Part 8 - Beacon (Hard)

### There's a flag being transmitted somewhere...

Here we can simply proceed from the autoruns_1_5ious step to the inetrun.exe binary in the Temp folder. If we dump the strings we see reference to a dll in the path:
> C:\Users\Administrator\AppData\Roaming\.cache\IECleanCache.dll

![sch_part_8_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_8_1.png?raw=true)

If we follow that path, and dump the strings on the IECleanCache.dll, we can retrieve the flag directly below the malicious url from earlier:

![sch_part_8_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_8_2.png?raw=true)

## SCH Part 9 - Parasite (Hard)

### I swear I'm not the one doing that, I'm legitimate! It's this thing, it's attached to me and I can't shake it!

### What is my name?

Here we can simply look at the parent process of olgreg.exe in Process Explorer. If we look at eplorer.exe and inspect the dlls, we can see the IECleanCache.dll has been injected into the process. The answer is the name of the process.

##### Note: This is an example of dll injection. For a more detailed explaination of this, Anthony from Level Effect recently did a walkthrough of another example of this that can be found [Here](https://www.youtube.com/watch?v=7fOa2IWZIck).


![sch_part_9](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_9.png?raw=true)

## SCH Part 10 - Slippery slug (Hard)

### I'm the parasite. What is my hash? (SHA-256)

Well this one is fairly easy, since we had already identified the malicious dll that was injected into explorer.exe, and have already identified the filepath. We can simply grab the hash and complete this challenge!

```ps
Get-FileHash .\IECleanCache.dll -Algorithm SHA256
```

![sch_part_10](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/sch_part_10.png?raw=true)

# Note: Dont forget to be a good Incident responder and clean up the system when you're done! We've identified all of the components so remove everything and make sure you didn't miss anything even if it isn't part of the challenge. ;)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/autoruns_1_5)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/)