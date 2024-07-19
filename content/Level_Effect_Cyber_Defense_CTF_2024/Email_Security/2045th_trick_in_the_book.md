---
title: "2045th trick in the book"
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Email_Security','Medium']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Email_Security](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/out_phishing)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Log_analysis/)

### This is a common encoding system that phishers abuse in their endless quest to bypass email scanners. Can you figure out what it is?

```
=C6=96=D0=B5=CE=BD=D0=B5=C6=96=D0=B5=C6=92=C6=92=D0=B5=D1=81=C5=A5{=D4=81=
=CE=BF=D5=B8=C5=A5=5F=D1=98=CA=8B=D1=95=C5=A5=5F=D1=81=CE=BF=D1=80=D1=83=5F=
=D1=80=D0=B0=D1=95=C5=A5=D0=B5=5F=C5=A5=C4=A7=D1=96=D1=95=5F=D1=96=D5=B8=
=C5=A5=CE=BF=5F=C5=A5=C4=A7=D0=B5=5F=D0=AC=CE=BF=D1=85}
```

We can paste this into [Cyberchef](https://cyberchef.org/) and use the 'magic' recipe to get the flag for this one!

![trick_in_the_book](https://github.com/jjolley91/blog/blob/main/static/le_ctf_24/trick_in_the_book.png?raw=true)


## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/email_security/out_phishing)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Log_analysis/)