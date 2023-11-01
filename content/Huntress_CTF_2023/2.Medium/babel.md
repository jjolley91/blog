---
title: "Babel"
date: 2023-10-17T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/rogue_inbox)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/indirect_payload) 

### It's babel! Just a bunch of gibberish, right? 

For this challenge we are given a file 'babel' to download. Inspecting the file reveals that it is heavily obfuscated with what looks like base64 encoding, and written in C#. The base64 encoding did not come out to anything usefull at this stage, and we ended up using an online [C# complier](https://www.programiz.com/csharp-programming/online-compiler/) tool to run the code, and modified the last few lines from:
```csharp
string YKyumnAOcgLjvK = "lQwSYRxgfBHqNucMsVonkpaTiteDhbXzLPyEWImKAdjZFCOvJGrU";

Assembly smlpjtpFegEH = Assembly.Load(Convert.FromBase64String(zcfZIEShfvKnnsZ(pTIxJTjYJE, YKyumnAOcgLjvK)));

MethodInfo nxLTRAWINyst = smlpjtpFegEH.EntryPoint;
nxLTRAWINyst.Invoke(smlpjtpFegEH.CreateInstance(nxLTRAWINyst.Name), null);
}
}
}
```
to include a print function to print the decoded lines:

```csharp
string YKyumnAOcgLjvK = "lQwSYRxgfBHqNucMsVonkpaTiteDhbXzLPyEWImKAdjZFCOvJGrU";

// Decoding the base64 string
string decodedString = zcfZIEShfvKnnsZ(pTIxJTjYJE, YKyumnAOcgLjvK);

// Printing the decoded values
Console.WriteLine("Decoded String: " + decodedString);

// Load the assembly
Assembly smlpjtpFegEH = Assembly.Load(Convert.FromBase64String(decodedString));

MethodInfo nxLTRAWINyst = smlpjtpFegEH.EntryPoint;
nxLTRAWINyst.Invoke(smlpjtpFegEH.CreateInstance(nxLTRAWINyst.Name), null);
}
}
}
```
We ran the compiler in the browser, and retrieved the output, which was further obfuscated with base64 encoding.

![babel1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/babel1.png?raw=true)


We then took the base64 encoded output, and decoded it to reveal that this is a compiled binary:

![babel2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/babel2.png?raw=true)

Luckliy, the flag for this challenge can be found in the strings of this output, or by saving it to a file and using:
```bash
strings decoded.exe | grep flag
```
![babel3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/babel3.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/rogue_inbox)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/indirect_payload)