---
title: "n00bCTF Web challenges"
date: 2023-05-25T13:25:32-05:00
tags: ['n00bCTF','Writeups', 'Web']
---
 
# [home](https://jjolley91.github.io/blog)

 # Intro

 These are the solutions I was able to find under the Web category. 
> Note: We are given a url to check out for each of these challenges.


 ### Club_n00b

 prompt: 
 ```
Can you get in the club? Author: 0xBlue
```
```url
http://challs.n00bzunit3d.xyz:8080/ 
```
Visiting the page we can see that we are not nearly radical enough for this flag. 

![club_n00b](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/club_n00b.png?raw=true)

You could use Burp for this, but it really isnt needed. 
I simply changed the secret_phrase from 'nope' to 'radical' in the address bar!

![change_radical](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/change_radical.png?raw=true)

```
Flag: n00bz{see_you_in_the_club_acting_real_nice}
```

### Robots

Prompt:
```
Dang, if only there was some standardized way to tell webcrawlers how to index your site. I guess we have to build our own :shrug: 
```
```URL
http://challs.n00bzunit3d.xyz:36083/robots
```

This one was very simple, the only requirement is to know about robots.txt files.

Web applications use this to tell search engines like Google not to show certain pages in the search results.

```
http://challs.n00bzunit3d.xyz:36083/robots.txt
```

```
Flag: n00bz{1_f0und_7h3_r0b0ts!}
```

### Secret Group

prompt:
```
To get the flag, you must be a member of the secret group! 
```

We can change that, I just opened up burp, sent the request to repeater and changed the user-agent string to n00bz_4dm1n.

We are then met with a series of other breadcrumbs which lead me to further modify the request.

I ended up with the final request of:

```HTML
GET / HTTP/1.1
Host: challs.n00bzunit3d.xyz:31401
User-Agent: n00bz-4dm1n
Accept: fl4g
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
DNT: 1
referer: s3cr3t.n00bz-4dm1n.xyz
Connection: s3cur3
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
Give-Flag: 7ru3
```
![Secret_group](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/Secret_group.png?raw=true)

```
Flag: n00bz{y0u_4r3_n0w_4_v4l1d_m3mb3r_0f_th3_s3cr3t_gr0up!}
```



### CaaS

prompt:

```
Curl as a Service is old, welcome to Certificate as a Service! Note: flag is in flag.txt
```

Clicking the link takes to a login page:

![CaaS](https://github.com/jjolley91/blog/blob/main/static/n00bCTF/CaaS.png?raw=true)

After some trial and error I entered a single ", and found the service returned the flag! Not sure why that worked though...

```
Flag: n00bz{5571_57r1k3s_4g41n_7a1b3f4e5e}
```

>Note: I found out after the fact that this challenge got broken somehow and was giving the flag in response to any input.