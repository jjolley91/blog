---
title: "Autoruns 1-5"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Incident_Response','Medium','Hard']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Incident_Response](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Incident_Response/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Incident_Response/newws_flash_1_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Incident_Response/sch)


#### All of the Autoruns challenges were done on the 'Autoruns Challenges' VM.

#### Attackers compromised this Windows host and riddled it with persistence mechanisms in a see-what-sticks effort to maintain a foothold on the system. Can you find the persistence mechanisms?


### Autoruns #1 (Medium)

So, For most of these, we'll be using Autoruns to identify the persistence mechanism, and then hunting down the flags from there. Looking in Autoruns, we see the first entry 'MicrosoftEdgeAutoConfigure' which seems to be pointing to C:\Windows\system32\cscript.exe. However, If we look in the bottom we can see that it is actually pointing to an init.vbs script in the C:\Users\Administrator\AppData\Local\Temp\ directory. 

![ar_1_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_1_1.png?raw=true)


Inspecting this file we see that it is writing an out.txt file in the same directory: 

![ar_1_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_1_2.png?raw=true)

Inspecting the out.txt  file, we see that it seems like some system enummeration has been going on, as we see the whoami command and output, as well as various enummeration results. At the bottom of the file we find our first flag:

![ar_1_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_1_3.png?raw=true)

### Autoruns #2 (Medium)

For the next persistence, we return to autoruns, and eventually find a CommandlineEventCustomer in the WMI Database Entries, which has a customer name that is a base64 encoded string. 

![ar_2_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_2_1.png?raw=true)

We can also find this by opening up a powershell window and using: 
```
Get-WmiObject -Namespace root\subscription -Class __EventFilter
```
Then decoding the command with: 

```powershell
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("bGV2ZWxlZmZlY3R7YW5vdGhlcl9vbmVfYml0ZXNfdGhlX2R1c3R9"))
```

![ar_2_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_2_2.png?raw=true)

### Autoruns #3 (Medium)

For the third persistence mechanism, we can see a 'Disk Cleanup' Scheduled Task in the Task Scheduler section. This stands out because it is calling a powershell command that is using both iex, and converting something from a base64 string:1

![ar_3_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_3_1.png?raw=true)

We can view the action taken by the Disc Cleanup task in the Task Scheduler, and see that it is pointing to a registry entry, and has some base64 encoding at the end:

![ar_3_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_3_2.png?raw=true)

We can also visit the path in the registry hive to find the value is also the base64 encoded flag:

![ar_3_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_3_3.png?raw=true)


```powershell
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("bGV2ZWxlZmZlY3R7aXRzX2JlY29taW5nX3NlbGZfYXdhcmV9"))
```

![ar_3_4](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_3_4.png?raw=true)

### Autoruns #4 (Medium)

For this next challenge, we will eventually notice an Unverified service in autoruns: "W64Time" that is pointing to C:\Windows\System32\w64time.dll. If you are famaliar with windows binaries, you might know that there is no 64 bit version of w32time.dll (the legitimate dll). We could also figure this out by submitting the hash to VT, which will give no results, or googling the name of the dll, which will point it out as a known malicious dll used by a specific APT group. 

![ar_4_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_4_1.png?raw=true)

If we run the dll and call the EntryPoint function, we receive a pop-up window that hints toward the name of the malware: TinyTurla


![ar_4_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_4_2.png?raw=true)

We can do a little research about this malware. You might come across one of several sites which would be helpful for this such as [This One](https://unit42.paloaltonetworks.com/turla-pensive-ursa-threat-assessment/) which mentions a created Registry key in the path: 

> HKLM\SYSTEM\CurrentControlSet\Services\W64Time\Parameters

![ar_4_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_4_3.png?raw=true)

In this registry entry, we will notice a 'Security' value of: 
```
=6G6=67764EL?@E0BF:E60HbaE:>6N
```
This does not appear to be base64 encoding, but we can decode it to get the flag instead using rot47. You can use [Cyberchef](https://cyberchef.org/) if you already knew this, or you can use this [Cipher Identifier](https://www.dcode.fr/cipher-identifier), which will identify the encoding and decode it for you:

![ar_4_4](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_4_4.png?raw=true)


### Autoruns #5 (Hard)

I will be honest, I got this one by just clicking on the recycle bin on the desktop, which opens a notepad with some base64 encoding that can be decoded to reveal some random text with the flag hidden somewhere inside.

![ar_5_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_5_1.png?raw=true)

We can see from process explorer this file is being opened from 

> C:\Users\Administrator\AppData\Local\Temp\96bf70e5-2edb-4054-a678-013f3697a13e\wn1AE41.tmp

![ar_5_3](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/ar_5_3.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Incident_Response/newws_flash_1_2)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Incident_Response/sch)

