---
title: "Press Play On Tape"
date: 2023-10-17T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/m_three_sixty_five)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/who_is_real) 

### While walking home through a dark alley you find an archaic 1980s cassette tape. It has "PRESS PLAY ON TAPE" written on the label. You take it home and play it on your old tape deck. It sounds awful. The noise made you throw your headphones to the floor immedately. You snagged a recording of it for analysis. 

For this challenge we are given an audio file to download "pressplayontape.wav". Which you should under no circumstances play with the volume turned on.

The key to this challenge is to be old enough to recognize that the name of this challenge is a reference to commodore 64 games. The Commodore 64 was an iconic home computer system from the early 1980s that used cassette tapes as a common storage medium for programs and games. When you loaded a game or program from a cassette tape on a C64, you typically saw the message "Press Play on Tape" on the screen.


![press_play1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/press_play1.png?raw=true)


The gimic here is to convert the .wav file into a .t64 file. to do this, we downloaded a few programs from [SourceForge](https://wav-prg.sourceforge.io/audiotap.html) specifically, you need to download the [WAV-PRG](https://sourceforge.net/projects/wav-prg/files/wav-prg/4.2.1/wavprg-4.2.1-win32.zip/download) and [Audiotap](https://sourceforge.net/projects/wav-prg/files/audiotap/2.2.1/audiotap-2.2.1-win32.zip/download}. They will come in the form of .zip archive. We moved the zips to a folder, and extracted the wav-prg, followed by the autiotap while choosing to replace all files that are duplicate.Then run the wavprg.exe and choose the option to convert the file to T64.


![press_play2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/press_play2.png?raw=true)


Then click ok, and choose the .wav file on the next screen, as well as the destination to save the output to. The result will be a .t64 file that you can retrieve the flag from using a few different methods. The easiest method would be to run strings on the file or view it in a text editor:

![press_play3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/press_play3.png?raw=true)

Alternatively, you could also use an online [Emulator](https://c64online.com/c64-online-emulator/). Simply upload the t64 file and type run in the console and it will print the flag!

![press_play4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/press_play4.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/m_three_sixty_five)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/who_is_real)