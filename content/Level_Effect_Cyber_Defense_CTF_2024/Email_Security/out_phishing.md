---
title: "Out Phishing"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Email_Security','Easy']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Email_Security](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/safe_for_emails)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/2045th_trick_in_the_book)

### A Goodcorp employee recently reported a phishing attempt to his company email address. We've provided the email headers for you to analyze. What country is the original sending server hosted in?

Here we are given a file to download: out_phishing.txt

From inspecting the email header, we note several strings encoded in base64. One of these: 

> U2V1IGxpbmsgdmFpIHZlbmNlciBlbSBicmV2ZSE=

decodes to: 

> Seu link vai vencer em breve!

which is Portugese, and translates to: "Your link will expire soon"

We also have an ipaddress from the original sender: 193[.]217.1.27, which we can check with [Domain Dossier](https://centralops.net/co/domaindossier.aspx), and look at the network whois record to reveal the country code: LT, which can be googled to find the answer: Lithuania


![out_phishing](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/out_phishing.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/safe_for_emails)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/2045th_trick_in_the_book)