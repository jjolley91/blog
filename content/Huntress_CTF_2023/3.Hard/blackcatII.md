---
title: "Black Cat II"
date: 2023-10-30T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Hard']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Hard Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard/crab_rave)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/3.hard) 

### Be advised analyst: BlackCat is back! And they're mad. Very mad. Help our poor user recover the images that they downloaded while browsing their favorite art site. Quickly!


The final challenge!!! For this one we are given the file 'blackcatII' to download and unzip. 

Once extracted, we are given the victim files, and the decryptor.exe, which takes the path to the victim files, and a 64 character password this time:

![blackcatii1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcatii1.png?raw=true)


This binary is written in .Net assembly, so we used [DNSpy](https://github.com/dnSpy/dnSpy) for analysis.  

After inspecting the binary, we found the interesting function called 'Decrypt Files':

![blackcatii2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcatii2.png?raw=true)

We came to understand that it was using the supplied key to decrypt the first file, and then using the sha256 of the decrypted file as the key to decrypt the next file.  

This is important information since we no longer need to figure out the original key, if we can only find the original decrypted image of the first file of the list, which in this case is:
```txt
A_Sunday_Afternoon_on_the_Island_of_La_Grande_Jatte_by_Georges_Seurat_5773ff06-a03e-401b-8914-6106bc277bfd_large.jpg
```
Luckily, this file has a very unique looking name. It still was not easy to find the image however. We began scouring the web for any place that was hosting the image, and checking the hashes to see if they would work...

Eventually, we found this [site](https://www.atxfinearts.com/blogs/news/100-most-famous-paintings-in-the-world) which contained the photo we needed.

#### Note: the file name and size matched, but instead of .jpg the extension was .webp. This does not change the hash value.

We then saved the photo, and extracted the hash with 
```ps
 Get-FileHash -Algorithm SHA256 -Path .\*
 ```

 ```txt
 hash- || 80D60BDDB3B57A28D7C7259103A514CC05507C7B9CF0C42D709BDC93FFC69191 || 
 ```

It is also important to note that we needed to remove this encrypted file from the victim folder for this to work properly so the program wouldn't try to decrypt that file with the hash and throw the whole chain off.

Once we did that, we simply pasted in the hash key and retrieved the flag!


![blackcatii3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/blackcatii3.png?raw=true)