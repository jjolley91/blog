---
title: "Batchfuscation"
date: 2023-10-23T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/snake_oil)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/bad_memory) 

### I was reading a report on past Trickbot malware, and I found this sample that looks a lot like their code! Can you make any sense of it?

For this challenge we are given a file 'batchfuscation' to download and deobfuscate.

We can see that this is a heavily obfuscated batch script. We began by starting from the top, and using find/replace to begin deobfuscating the initial variables:

```txt
set bdevq=set  
set grfxdh=   
set mbbzmk==  
set xeegh=/  
set jeuudks=a  
set rbiky=c  
set wzirk=m  
set naikpbo=d  
set ltevposie=e  
set uqcqswo=x  
set zvipzis=i  
set kquqjy=t  
set kmgnxdhqb=   
```
After that the file looked like this:

![batchfuscation3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/batchfuscation3.png?raw=true)


From here, we took a slightly different approach. We decided to begin decodeing each line by including the following lines in the file, and running it in powershell to view the decoded output line by line:
```batch
echo :: whateverline
exit /b 0
```

![batchfuscation2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/batchfuscation2.png?raw=true)


Eventually, you will see a set with : 'flag_characterxx=y'. We can do a find all in current document search, and then copy every instance of flag_character, then paste that in and echo each value when we run the program again: 

![batchfuscation4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/batchfuscation4.png?raw=true)


we get the characters for the flag:

```txt 
20=3  
34=d  
23=c  
30=0  
22=a  
15=0  
38=}  
27=9  
31=d  
21=1  
36=9  
12=e  
7=c  
17=5  
26=3  
11=7  
29=6  
8=a  
10=6  
35=1  
37=a  
18=b  
32=b  
14=d  
16=b  
9=d  
6=a  
24=6  
28=3  
19=f  
33=9  
13=3  
25=6  
```

Finally, we placed the values in a flag file, and ran the following command to extract the flag in one line:

```bash
echo "$(cat flag | sort -V | cut -d '=' -f2 | tr -d '\n')"
```
![batchfuscation5](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/batchfuscation5.png?raw=true)


Alternatively, you could add an 'echo ' to the beginning of every line after line 224 (assuming you're working with the un-edited file) 
![batchfuscation6](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/batchfuscation6.png?raw=true)


Then run the file like so: 

```powershell
.\batchfuscation.bat | Select-String -Pattern "^:: set flag.*$" | Sort-Object { [int]($_ -replace '\D', '') } | ForEach-Object { $_.Line -replace '^.*character(\d+)=(.)', '$1 $2' } | Sort-Object { [int]($_.Split(' ')[0]) } | ForEach-Object { $_.Split(' ')[1] }| ForEach-Object { Write-Host -NoNewline $_ }
```

![batchfuscation7](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/batchfuscation7.png?raw=true)


### Here is an interesting link to a writeup of this type of batch obfuscation being used maliciously in the wild:  

####  Tried and true hacker technique: [DOS obfuscation](https://www.huntress.com/blog/tried-and-true-hacker-technique-dos-obfuscation ) .Hammond, J. (n.d.). 


## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/snake_oil)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/bad_memory)