---
title: "MFAtigue"
date: 2023-10-27T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/bad_memory)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/snake_eaterii) 

### We got our hands on an NTDS file, and we might be able to break into the Azure Admin account! Can you track it down and try to log in? They might have MFA set up though...

For this challenge, we are given a webserver to spin up, as well as NTDS.zip to download.

Once we extract the archive, we receive ntds.dit and SYSTEM. We can use [dsinternals](https://www.dsinternals.com/en/) to  assist with the analysis and the module can be installed by running the following command in a powershell window running as administrator:

```ps
Install-Module -Name DSInternals -Force
```

We can then get the account information from the active directory database (NTDS.dit) using the following command to output the result to a .txt file:

```ps
Get-ADDBAccount -All -DBPath .\ntds.dit -Bootkey "$(Get-BootKey -SystemHivePath .\SYSTEM)" > .\output.txt
```
We know we need to find an Azure admin, so we can search for that within the document, and we get one single result:

![mfatigue1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/mfatigue1.png?raw=true)

We now know the username, and we can retrieve the password by cracking the NTLM hash. We used [crackstation](https://crackstation.net/) for this.

```txt
08e75cc7ee80ff06f77c3e54cadab42a = katlyn99
```

We can now spin up the webserver and try logging in with the credentials:

#### huntressctf\Jillian_Dotson  
#### katlyn99  


We are then taken to a screen and have to wait for the sign in request to be approved. 

![mfatigue2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/mfatigue2.png?raw=true)

However, if we remember the name of this challenge, we can keep sending push notifications, and eventually retrieve the flag!


![mfatigue3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/mfatigue3.png?raw=true)


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/bad_memory)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/snake_eaterii)