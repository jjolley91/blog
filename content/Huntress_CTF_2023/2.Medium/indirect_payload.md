---
title: "Indirect Payload"
date: 2023-10-18T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/babel)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/thumb_drive) 

### We saw this odd technique in a previous malware sample, where it would uncover it's next payload by... well, you'll see.

Here we are given a webserver to spin up.  

Upon visiting the webpage we see a button that says "retrieve the payload". Upon clicking the button we are redirected to a bunch of php pages only to eventually land on a "We're Sorry!" message.  
### Note: We solved this solution two different ways:

# Method 1
After some trial and error, we decided to use WireShark to create a pcap of the traffic generated from clicking the button. 


![indirect1.png](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/indirect1.png?raw=true)


If we start with the flag.php request and follow the http stream we can see the responses from the server. After some poking around we noticed that every other response contained a short message: 'character n of the payload is x'

![indirect2.png](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/indirect2.png?raw=true)


If we followed this all the way down, we found that we are only given the first 18 characters of the flag from this stream. We decided to then to copy all of the http stream to a text document, and then filter out the stream in wireshark. We then moved on to follow the next http stream to get the next characters of the flag, and repeated the process with the third and final stream. We dumped all of the streams to a txt file, and used the following command to more easily retrieve the flag:

```bash
cat dump | grep -E 'character [0-9]+ of the payload is [0-9a-z\{\}]+$' | awk '{print substr($0,length,1)}' | tr -d '\n'
```

Or in powershell:
```ps
$flag = @(); cat .\dump_flag.txt | Select-String -Pattern '^character [0-9]+ of the payload is ([0-9a-z\{\}]+)$' | % { $flag += $_.Matches.Groups[1].Value }; $flag -Join '';
```

![indirect3.png](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/indirect3.png?raw=true)

# Method 2:
We also found another way of getting the flag using only the command line. First, set the port number to the variable $Port 
### Example:
```bash
Port=1337
```
Then run the following commands:
```bash
wget http://chal.ctf.games:$Port/site/
```
```bash
cat index.html | cut -f 8 -d '"' | grep .php > urls
```
```bash
sed -i "s|^|http://chal.ctf.games:$Port/site/|" urls
```
```bash
for i in $(cat urls); do curl $i; done | 2>&1 >  flag 
```
```bash
cat flag | sort -V | grep -o '.$' | tr -d '\n'
```
![indirect4.png](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/indirect4.png?raw=true)


Or you could do it in one line, like so (Don't forget to replace the 'port' with the port number you are given):
```bash
port='11111';url="http://chal.ctf.games:${port}/site/"; for uri in $(wget -nv -O - $url > /dev/null | cut -f 8 -d '"' | grep -E '[0-9a-f]{32}\.php'); do curl -Ss "${url}${uri}" >> flag.txt; done; cat flag.txt | sort -V | grep -o '.$' | tr -d '\n'
```

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/babel)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/thumb_drive)