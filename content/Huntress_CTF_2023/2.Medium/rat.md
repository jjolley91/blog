---
title: "Rat"
date: 2023-10-21T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/speakfriend)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/snake_oil) 

###  I was arguing with a co-worker on whether or not it is "Remote Access Tool" or "Remote Access Trojan", and he didn't agree with me, so I sent him this shady file ;) 

#### Note: We found two ways to solve this challenge, one is easier than the other.

## Method 1: 
To begin, we are given a binary 'rat' to download and inspect. After some analysis, we find that this is a .NET assembly, and we were able to use [dnSpy](https://github.com/dnSpy/dnSpy) to decompile the binary to see what it was doing. We found that it was decrypting some hex bites using a key, and using gzip Decompress to pull in another binary:

```.NET
// Token: 0x0600002F RID: 47 RVA: 0x000028B4 File Offset: 0x00000AB4
public static byte[] decrypt(byte[] data, int pass)
{
	for (int i = 0; i < data.Length; i++)
	{
		data[i] = (byte)((int)data[i] ^ pass);
	}
	byte[] result;
	using (MemoryStream memoryStream = new MemoryStream(data))
	{
		using (GZipStream gzipStream = new GZipStream(memoryStream, CompressionMode.Decompress))
		{
			using (MemoryStream memoryStream2 = new MemoryStream())
			{
				gzipStream.CopyTo(memoryStream2);
				result = memoryStream2.ToArray();
			}
		}
	}
	return result;
```

We set a breakpoint at the result, and ran the binary in debug mode so we could see what the decompressed data looked like.


![rat1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rat1.png?raw=true)


We can tell that this is another executable by the first few bites being 0x4D and 0x5A. We then saved the decompressed binary, and loaded it into dnspy for inspection. We found a flag variable which was present, but not being decrypted in the program.

![rat3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rat2.png?raw=true)

We ended up changing one of the values which was being decrypted, to decrypt the flag instead. Then saved the patched binary, and reloaded it into dnSpy. From there we were able to set a breakpoint at the section which decrypts the flag, and view the result!

![rat3](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rat3.png?raw=true)


![rat4](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rat4.png?raw=true)

# Method 2: 
The easier method was to upload the sha526 hash to Virus total and inspect the 'Details' tab:

![rat2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rat.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/speakfriend)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/snake_oil) 
