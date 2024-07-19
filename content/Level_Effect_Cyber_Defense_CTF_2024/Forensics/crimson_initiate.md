---
title: "Crimson Initiate"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Forensics','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Forensics](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/puzzle_pieces)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/)

#### NOTE - The resources needed for this challenge are on the Cyber Defense CTF Triage Workstation VM on our hosted platform.

### Let's dabble a bit on the offensive side. There is a user named crimson with admin privileges on the Triage Workstation. Use any method you prefer to get the user's password. The password is the flag.

#### You are able to download tools to the workstation if need be

For this challenge we are directed again to the Cyber Defense CTF Triage Workstation, and told that there is a user on the system named 'Crimson'. The objective is to retrieve their password. 

We can do this quite easily if we use [Mimikatz](https://github.com/gentilkiwi/mimikatz/releases/tag/2.2.0-20220919)!

Once mimikatz is downloaded and extracted, we can open a cmd prompt as the System user:

```powershell
psexec -i -s cmd.exe
```

Then we can start mimikatz and dump the NTLM hashed passwrods for all the users and look for the user Crimson.

```cmd
.\mimikatz.exe

privilege::debug

lsadump::sam
```

![crimson_initate_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/crimson_initate_1.png?raw=true)

Now that we have the NTLM hash all we need to do is crack it using your software of choice. I went with [Crackstation](https://crackstation.net/) for this, which cracked the hash without any issue, since it was a weak password.

![crimson_initate_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/crimson_initate_2.png?raw=true)


#### Note: This flag does not need to be in the leveleffect{} wrapper.

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Forensics/puzzle_pieces)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/)