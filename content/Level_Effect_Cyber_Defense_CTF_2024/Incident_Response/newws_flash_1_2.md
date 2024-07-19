---
title: "Newws Flash 1 & 2"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Incident_Response','Easy', 'Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Incident_Response](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/autoruns_1_5)

## Newws Flash 1

### Our detections hit on the file hash [b1f2068201c29f3b00aeedc0911498043d7c204a860ca16b3fef47fc19fc2b22](). Can you determine what malware family this sample belongs to?

#### WARNING - the sample referenced is actual malware seen in the wild. If you choose to analyze the sample yourself, make sure you know what you're doing and take care to follow proper handling procedure.

For this challenge, we can simply upload the given hash to [VirusTotal](https://www.virustotal.com/gui/file/b1f2068201c29f3b00aeedc0911498043d7c204a860ca16b3fef47fc19fc2b22) And find the malware family in the results. Pretty straightforward.

![newws_flash_1](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/newws_flash_1.png?raw=true)



## Newws Flash 2

### Our detections hit on the file hash [b1f2068201c29f3b00aeedc0911498043d7c204a860ca16b3fef47fc19fc2b22](). The sample is observed to create a registry Run key under HKCU. Can you find the name of the file that key is set to execute?

We can follow the same process for this challenge as in Newws Flash 1, Upload the hash to [VirusTotal](https://www.virustotal.com/gui/file/b1f2068201c29f3b00aeedc0911498043d7c204a860ca16b3fef47fc19fc2b22/behavior), and view the results. This time, we need to go to the 'Behavior' tab, and look for the the 'Registry Keys Set' section and find the name of the file it creates in the HKCU Registry Run key.


![newws_flash_2](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/newws_flash_2.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/incident_response/autoruns_1_5)