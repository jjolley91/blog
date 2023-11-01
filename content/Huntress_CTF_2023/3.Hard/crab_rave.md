---
title: "Crab Rave"
date: 2023-10-29T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Hard']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Hard Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/chainsaw_massacre)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/blackcatii) 

### My biologist friend told me that everything eventually evolves into a crab-like form. I don't know if that's true but I guess malware authors got a head start on that evolution. To save you some time, I went ahead and found you the 10 hour extended version of Crab Rave on YouTube (https://www.youtube.com/watch?v=-50NdPawLVY). You'll need it.

### So, here's the deal. This one is tough, so we're giving you a "Choose Your Own Adventure" challenge. Are you super confident with reverse engineering? Try crab_rave_harder.7z. Not so confident with RE? We gave you crab_rave_easier.7z.

### Both have the same flag. Both do the same thing. If you solve one, you solve both. No matter which one you go with, it will be challenging. You got this.

While the hard version is intriguing, we opted for the easy option in the interest of time.

Downloading the provided crab_rave_easier.7z archive and extracting it gives us a DLL and a Windows LNK (shortcut) file amusingly labeled "SAFE_NO_VIRUSES".

![crab_rave1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave1.png?raw=true)

We started with the LNK file, using the tool [LnkParse3](https://github.com/Matmaus/LnkParse3) to find its target program and command line arguments. The shortcut points to cmd.exe which proxy executes the provided ntcheckos.dll via rundll32.exe after some ping sleeps. Particularly, it loads the function DLLMain, something odd to see since DllMain is a method of entry into a DLL that wouldn't customarily be directly called.

![crab_rave2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave2.png?raw=true)

Moving onto the DLL, we load it into Ghidra and analyze it. Some of the decompiled code suggests that this binary is written in Rust, hence the challenge name. In the symbol tree we discover two similar functions - DllMain and DLLMain.

![crab_rave3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave3.png?raw=true)

At this point we understood that DLLMain is a custom function masquerading as DllMain. It is also the one executed by the Windows shortcut seen before.

Focusing on DLLMain, we saw that it calls NtCheckOSArchitecture(). Towards the bottom of that function we spotted an interesting function named inject_flag().

![crab_rave4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave4.png?raw=true)

Drilling down further into inject_flag(), we found that the function performs a web request and feeds the response to an AES-256 CBC decryptor. The key and IV are hardcoded in.

![crab_rave5](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave5.png?raw=true)

We suspected that the decrypted output would reveal the flag. Now aware of where to look, we pivoted to dynamic analysis with x64dbg.

To streamline analysis and standardize the memory addresses between Ghidra and x64dbg, we first rebased the DLL in Ghidra to match its load address observed in x64dbg.
!!! Ask if OK !!! A better method we could have used is to disable the DLL's ASLR in CFF Explorer before loading it in the debugger. All memory offsets included from here on will be based on this.

![crab_rave6](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave6.png?raw=true)

The goal was to call function inject_flag() and step through to observe what data gets returned from the aforementioned web request. We copied the function's memory address @ 0x000000001000A200 in Ghidra and overwrote the DLL EntryPoint's first instruction with call 0x000000001000A200 to immediately call that address upon execution.

![crab_rave7](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave7.png?raw=true)

We enabled a breakpoint on the EntryPoint, ran it, and stepped into the call. At this point we had issues making the web request work, but it proved no matter since we could observe the request URL https://gist.githubusercontent.com/HuskyHacks/8cece878fde615ef8770059d88211b2e/raw/abcaf5920a40843851eec550d1dca97e9444ac75/gistfile1.txt stored in RSI and RDX registers right before the web request executes by setting and running up until a breakpoint @ 0x000000001000A262.

![crab_rave8](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave8.png?raw=true)

We curled the URL and received the ciphertext.

![crab_rave9](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave9.png?raw=true)

Since we had the ciphertext, decryption key, and IV we were able to manually decrypt the ciphertext using [this site](https://encode-decode.com/aes-256-cbc-encrypt-online/). The decrypted text contained the flag!

![crab_rave10](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave10.png?raw=true)

Alternatively, the following CyberChef recipe can be used:
```txt
From_Base64('A-Za-z0-9+/=',true,false)
AES_Decrypt({'option':'UTF8','string':'rAcbUUWWNFlqMbruiYOIsAyVQHS78orv'},{'option':'UTF8','string':'MoJ8C6O4D3asAApB'},'CBC','Raw','Raw',{'option':'Hex','string':''},{'option':'Hex','string':''})
Regular_expression('User defined','flag\\{[a-f0-9]+\\}',true,true,false,false,false,false,'List matches')
```
![crab_rave11](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/crab_rave11.png?raw=true)



## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/chainsaw_massacre)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/blackcatii) 