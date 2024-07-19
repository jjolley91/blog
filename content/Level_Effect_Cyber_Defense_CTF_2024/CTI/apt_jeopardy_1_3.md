---
title: "APT Jeopardy 1, 2, & 3"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','CTI','Medium','Hard','Written_by_me']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [CTI](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/CTI/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/CTI/got_my_tail)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/)


#### Note: I only wrote jeopardy questions 2 & 3.

## APT jeopardy 1 (Medium)

### This state-sponsored APT has been known for its cyber-espionage and disruptive operations that target defense, telecom and critical infrastructure primarily in the US. The group is believed to have surfaced in 2021.

### One of the APT's hallmark TTPs is living off the land to blend into target environments. One of its most unique TTPs is proxying operational traffic through compromised VPSs and SOHO network devices so as to obscure the true origin of the activity.

### Name the APT!

For this one, as with most of the CTI challenges, you can simply do a bit of research. Googling something like: "APT targeting Critical US infrastructure using living off the land binaries" Should lead you to a site such as [this one](https://www.microsoft.com/en-us/security/blog/2023/05/24/volt-typhoon-targets-us-critical-infrastructure-with-living-off-the-land-techniques/), where you can quickly discover the name of the group!

## APT jeopardy 2 (Medium)
### Goodcorp recently suffered a data breach. The nature of the breach and the sophisticated tactics observed suggest the threat actor is likely an APT. The Incident Response team collected the following from its investigation:

* The initial point of compromise was a spearphishing email.
* The email was designed to mimic an MFA alert and contained a malicious QR code.
* The link in the QR code led to the site thepiratecinemaclub[.]org NOTE: Do not attempt to visit this site.
* Once on the system, a persistence mechanism in the form of a modified version of CpuTrace was dropped.
* We found artifacts of a C2 proxy known as XTunnel on compromised systems.

### There are more pressing matters than attribution here, but for the purposes of the challenge, name the APT!

Here we are given several ttps used by the group, A big lead in this case is the use of QR codes.

We can also use [VirusTotal](https://www.virustotal.com/gui/url/f4ad10711c2ec38cc9aeb26d2c3acaaf892fa669612d459b5900b51846d13217/community) for this one since we are given a domain. Looking up the domain and going to the community tab will quickly give us the name of this APT!



## APT jeopardy 3 (Hard)
### Aerocorp, a subsidiary of Goodcorp, recently suffered a massive data breach by a sophisticated actor. Can you identify the group responsible?

* We believe employee credentials were initially compromised via spearphishing campaign.
* A handful of employees were social engineered into clicking on malicious attachments.
* The use of Cobalt Strike was observed in post-compromise network traffic.
* Operations found post-compromise PowerShell activity consistent with the PowerSploit framework.
* The attackers scheduled remote AT jobs via commandline.
* Forensics recovered a binary created around the time of compromise with the hash 40528e368d323db0ac5c3f5e1efe4889.
* Logged network traffic reveals that images with unusually large file sizes were uploaded to various GitHub accounts.

### Name the APT!


For this challenge, again, we can do some research. These given indicators are fairly vague though, as many APTs are known to use these ttps. However, we are also given a file hash which looks interesting. If we upload the hash to [VirusTotal](https://www.virustotal.com/gui/file/b731b4871f95c51ac47a3fa3fdc0704e624b0e923dc327af371dd851625646dd/detection), we will see that the name of the file is mt.exe. Some further research will show that this is MURKYTOP. This will ultimately lead us to the name of the group we are looking for.


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/CTI/got_my_tail)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/)