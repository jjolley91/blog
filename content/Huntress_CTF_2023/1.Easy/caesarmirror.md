---
title: "CaesarMirror"
date: 2023-10-05T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Warmups', 'Easy']
---
 
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/BaseFFFF+1)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/i_wont_let_you_down) 

### Caesar caesar, on the wall, who is the fairest of them all?

#### Perhaps a clever ROT13?

Here we are given a text file named 'caesarmirror.txt' to download.
Opening the file in a text editor we are greeted with the following passage:
```txt
     Bu obl! Jbj, guvf jnezhc punyyratr fher   bf V !erugrtbg ghc bg ahs sb gby n fnj 
    qrsvavgryl nofbyhgryl nyjnlf ybir gelvat   ftavug rivgnibaav qan jra ch xavug bg 
       gb qb jvgu gur irel onfvp, pbzzba naq   sb genc gfevs ruG !frhdvauprg SGP pvffnyp 
     lbhe synt vf synt{whyvhf_ naq gung vf n   tavuglerir gba fv gv gho gengf gnret 
 gung lbh jvyy arrq gb fbyir guvf punyyratr.    qan rqvu bg tavleg rxvy g'abq V 
  frcnengr rnpu cneg bs gur synt. Gur frpbaq   bq hbl gho _n_av fv tnys rug sb genc 
   arrq whfg n yvggyr ovg zber. Jung rknpgyl   rxnz qan leg bg reru rqhypav rj qyhbuf 
     guvf svyyre grkg ybbx zber ratntvat naq   ?fravyjra qqn rj qyhbuF ?ryvujugebj 
    Fubhyq jr nqq fcnprf naq gel naq znxr vg   uthbar fv fravy lanz jbU ?ynpvegrzzlf 
 gb znxr guvf svyyre grkg ybbx oryvrinoyr? N    n avugvj ferggry sb renhdf qvybf 
 fvzcyr, zbabfcnpr-sbag grkg svyr ybbxf tbbq   rug gn gfbzyn rj reN .rz bg uthbar 
   raq? Vg ybbxf yvxr vg! V ubcr vg vf tbbq.   }abvgprysre fv tnys ehbl sb genc qevug ruG 
naq ng guvf cbvag lbh fubhyq unir rirelguvat   ebs tnys fvug gvzohf bg qrra hbl gnug 
    cbvagf. Gur ortvaavat vf znexrq jvgu gur   ,rpneo lyehp tavarcb rug qan kvsrec tnys 
  naq vg vapyhqrf Ratyvfu jbeqf frcnengrq ol   lyehp tavfbyp n av qar bg ,frebpferqah 
  oenpr. Jbj! Abj GUNG vf n PGS! Jub xarj jr   fvug bg erucvp enfrnp rug xyvz qyhbp 
            rkgrag?? Fbzrbar trg gung Whyvhf   !ynqrz n lht enfrnP 
```

Taking the hint from the challenge description, we can try putting this through a ROT13 cypher.

A ROT13 (Rotate by 13 places) cipher is a simple letter substitution cipher that is a type of Caesar cipher. In a Caesar cipher, each letter in the plaintext is shifted a certain number of places down or up the alphabet. In the case of ROT13, it's a special case of the Caesar cipher where each letter is shifted 13 positions. It's a symmetric cipher because applying ROT13 a second time to the ciphertext will decode it, i.e., ROT13(ROT13(text)) = text.

Here's how the ROT13 cipher works:

It only applies to letters. Digits, symbols, and spaces are not shifted.

Each letter is replaced by the letter 13 positions down the alphabet. For example:
```txt
'A' becomes 'N'
'B' becomes 'O'
'C' becomes 'P'
...etc
```
By applying this to the text (I used [CyberChef](https://cyberchef.org/) for this entire solution), we get this result:
```txt
     Oh boy! Wow, this warmup challenge sure   os I !rehtegot tup ot nuf fo tol a saw 
    definitely absolutely always love trying   sgniht evitavonni dna wen pu kniht ot 
       to do with the very basic, common and   fo trap tsrif ehT !seuqinhcet FTC cissalc 
     your flag is flag{julius_ and that is a   gnihtyreve ton si ti tub trats taerg 
 that you will need to solve this challenge.    dna edih ot gniyrt ekil t'nod I 
  separate each part of the flag. The second   od uoy tub _a_ni si galf eht fo trap 
   need just a little bit more. What exactly   ekam dna yrt ot ereh edulcni ew dluohs 
     this filler text look more engaging and   ?senilwen dda ew dluohS ?elihwhtrow 
    Should we add spaces and try and make it   hguone si senil ynam woH ?lacirtemmys 
 to make this filler text look believable? A    a nihtiw srettel fo erauqs dilos 
 simple, monospace-font text file looks good   eht ta tsomla ew erA .em ot hguone 
   end? It looks like it! I hope it is good.   }noitcelfer si galf ruoy fo trap driht ehT 
and at this point you should have everything   rof galf siht timbus ot deen uoy taht 
    points. The beginning is marked with the   ,ecarb ylruc gninepo eht dna xiferp galf 
  and it includes English words separated by   ylruc gnisolc a ni dne ot ,serocsrednu 
  brace. Wow! Now THAT is a CTF! Who knew we   siht ot rehpic raseac eht klim dluoc 
            extent?? Someone get that Julius   !ladem a yug raseaC 
```

This is only the first part of the solution, as we are only given the first part of the flag, and the second half seems to still be illegible. We are, given another hint in the second part of the name of this challenge. If we take the second half of the passage and 'mirror' (reverse) it we are able to read the second half.

```txt
 Caesar guy a medal!   					suiluJ taht teg enoemoS ??tnetxe            
 could milk the caesar cipher to this   ew wenk ohW !FTC a si TAHT woN !woW .ecarb  
 underscores, to end in a closing curly   yb detarapes sdrow hsilgnE sedulcni ti dna  
 flag prefix and the opening curly brace,   eht htiw dekram si gninnigeb ehT .stniop    
 that you need to submit this flag for   gnihtyreve evah dluohs uoy tniop siht ta dna
 The third part of your flag is reflection}   .doog si ti epoh I !ti ekil skool tI ?dne   
 enough to me. Are we almost at the   doog skool elif txet tnof-ecapsonom ,elpmis 
 solid square of letters within a    A ?elbaveileb kool txet rellif siht ekam ot 
 symmetrical? How many lines is enough   ti ekam dna yrt dna secaps dda ew dluohS    
 worthwhile? Should we add newlines?   dna gnigagne erom kool txet rellif siht     
 should we include here to try and make   yltcaxe tahW .erom tib elttil a tsuj deen   
 part of the flag is in_a_ but you do   dnoces ehT .galf eht fo trap hcae etarapes  
 I don't like trying to hide and    .egnellahc siht evlos ot deen lliw uoy taht 
 great start but it is not everything   a si taht dna _suiluj{galf si galf ruoy     
 classic CTF techniques! The first part of   dna nommoc ,cisab yrev eht htiw od ot       
 to think up new and innovative things   gniyrt evol syawla yletulosba yletinifed    
 was a lot of fun to put together! I so   erus egnellahc pumraw siht ,woW !yob hO  
```
From here we are able to piece together, and submit the flag!
```txt
Oh boy! Wow, this warmup challenge sure 
was a lot of fun to put together! I so
definitely absolutely always love trying 
to think up new and innovative things
to do with the very basic, common and 
classic CTF techniques! The first part of
your flag is flag{julius_ and that is a 
great start but it is not everything
that you will need to solve this challenge.
I don't like trying to hide and
separate each part of the flag. The second  
part of the flag is in_a_ but you do
need just a little bit more. What exactly
should we include here to try and make
this filler text look more engaging and
worthwhile? Should we add newlines?
Should we add spaces and try and make it 
symmetrical? How many lines is enough
to make this filler text look believable? A 
solid square of letters within a
simple, monospace-font text file looks good  
enough to me. Are we almost at the
end? It looks like it! I hope it is good. 
The third part of your flag is reflection}
and at this point you should have everything  
that you need to submit this flag for
points. The beginning is marked with the 
flag prefix and the opening curly brace,
underscores, to end in a closing curly 
brace. Wow! Now THAT is a CTF! Who knew we  
could milk the caesar cipher to this
extent?? Someone get that Julius
Caesar guy a medal! 
 ```

 ## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/BaseFFFF+1)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/i_wont_let_you_down) 