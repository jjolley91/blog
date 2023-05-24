---
title: "JuiceShop"
date: 2023-05-23T17:05:16-05:00
---

![Img](https://github.com/jjolley91/blog/blob/main/images/juice_shop.jpg?raw=true)

First of all, if you're reading this, thank you! This is my writeup for the vulnerable web app Juice Shop. There are a TON of vulnerabilities to go through here. My goal is to go over each one, provide the steps I used to solve them, and document my thought process along the way.

I've listed the challenges in order by difficulty level 

# Intro:

The first thing that jumped out at me upon visiting the page was the account section, as well as the search bar:
![landing screenshot](https://github.com/jjolley91/blog/blob/main/images/landing_page.png?raw=true)


After some poking around I decided to try logging in. I decided to see if the site would be vulnerable to sql injection.

>email: 'or 1=1--

>password: q


![sql_login](https://github.com/jjolley91/blog/blob/main/images/sql_login.png?raw=true)

**Note:** Accepting the cookies is a good idea here.

After hitting enter I was successfully logged in as ADMIN?!

The reason this worked has to do with the imput not being properly sanitized before going to the sql db. Normally the program would be doing something like:

```SQL
SELECT user_id FROM users_table WHERE email_address = 'some@valid.email'  AND password = 'password';
```
However, without being properly handled the query itself can be manipulated so instead of properly checking we escaped the query with the single quote, then added a statement which will always evaluate to 'True'. 
We end up with the query:

```SQL
SELECT user_id FROM users_table WHERE email_address = '' OR 1=1--' 

```
Thus we end up canceling the original query and the system just returns the first user in the database, which is usually an admin account! Pretty neat!

So we now have the Admin email as: admin@juice-sh.op

![admin_email](https://github.com/jjolley91/blog/blob/main/images/admin_email.png?raw=true)


OK, Still just poking around on my own I eventually clicked on the 'Help getting started' which gave a pop-up with a few interesting hints such as:

>You find the JavaScript code in the DevTools of your browser that will open with F12.
		
>Look through the client-side JavaScript in the Sources tab for clues. Or just start URL guessing. It's up to you!

>This application is riddled with security vulnerabilities. Your progress exploiting these is tracked on a Score Board.

>You won't find a link to it in the navigation or side bar, though. Finding the Score Board is in itself actually one of the hacking challenges.


I looked in Dev tools< Debugger (right click the screen, then choose inspect) and searched (ctrl+f) for 'Score'  which gave me:

```js
path: 'score-board'
```
![debugger_search](https://github.com/jjolley91/blog/blob/main/images/debugger_search.png?raw=true)


I then just decided to try searching for 'Path', as a rudimentary directory fuzzing technique. I was rewarded with a nice list of directories to check out while going through the rest of the challenges.
```js

        path: 'administration',

        path: 'accounting',

        path: 'about',
 
        path: 'address/select',

        path: 'address/saved',

        path: 'address/create',

        path: 'address/edit/:addressId',

        path: 'delivery-method',

        path: 'deluxe-membership',
        component: (() =>{
          class o {
            constructor(e, n, i, r, l, u, f) {
              this.router = e,
              this.userService = n,
              this.cookieService = i,
              this.configurationService = r,
              this.route = l,
              this.ngZone = u,
              this.io = f,
              this.membershipCost = 0,
              this.error = void 0,
              this.applicationName = 'OWASP Juice Shop',
              this.logoSrc = 'assets/public/images/JuiceShop_Logo.png'
            }

		path: 'saved-payment-methods',

        path: 'basket',
 
        path: 'order-completion/:id',

        path: 'contact',

        path: 'photo-wall',
 
        path: 'complain',

        path: 'chatbot',

        path: 'order-summary',

        path: 'order-history',

        path: 'payment/:entity',

        path: 'wallet',

        path: 'login',

        path: 'forgot-password',
 
        path: 'recycle',

        path: 'register',

        path: 'search',

        path: 'hacking-instructor',

        path: 'score-board',

        path: 'track-result',

        path: 'track-result/new',

        path: '2fa/enter',

        path: 'privacy-security',

		path: 'privacy-policy',

		path: 'change-password',

		path: 'two-factor-authentication',

		path: 'data-export',

		path: 'last-login-ip',
```

Thats a lot of paths to check out!
I will refer back to the list as I go or if I get stuck, for now I decided to see what the 'Score-board' page was all about.

>http://juiceshop-ip-address/#/score-board/

![score-board-page](https://github.com/jjolley91/blog/blob/main/images/scoreboard_page.png?raw=true)


By this point it shows I have completed 1 level 1 challenge and one level 2 challenge, but from here on I will attempt to solve these in the order they appear by difficulty.

# Level  1

the first challenge appears to be an additional part of the DOM XSS challenge, so I'll solve these two together, as the script for both are listed, this is easy if you are famaliar with XSS methods.


#### DOM XSS

> Perform a DOM XSS attack with 
```html
<iframe src="javascript:alert(`xss`)">
```

XSS stands for cross site-scripting, and arises when JavaScript is able to take data from a user source, such as a search bar, or url.

Since they were nice enough to simply provide the exact command, I just pasted it into the search bar:

![xss_search](https://github.com/jjolley91/blog/blob/main/images/xss_search.png?raw=true)

##### *Note* : the box that appears just contains 'xss', but could contain any other string/malicious code.

![xss_result](https://github.com/jjolley91/blog/blob/main/images/xss_result.png?raw=true)

also note the areas where the query is visible, this could have also been executed by typing 
```html
/search?q=<iframe src="javascript:alert(`xss`)">
```
directly in the address bar!


#### Bonus Payload

>Use the bonus payload 
```html
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
 ```
>in the DOM XSS challenge.

![bonus_xss_result](https://github.com/jjolley91/blog/blob/main/images/bonus_xss_result.png?raw=true)


This command redirects to a soundcloud api and plays the catchy Juice Shop Jingle, which has been stuck in my head for a week now. This is an excellent example of how this type of vulnerability can be used to wreak havoc on improperly coded sites.


#### Bully Chatbot

> Receive a coupon code from the support chatbot.

This seems to direct me to the support chat section.

![support_location](https://github.com/jjolley91/blog/blob/main/images/support_location.png?raw=true)

The chatbot asks for your name, i named myself coupon.
![support_name](https://github.com/jjolley91/blog/blob/main/images/support_name.png?raw=true)

 I kept asking for a coupon but kept getting a no from the chatbot. However, the category for this challenge was **Brute force**, so I just kept asking coupon related questions. Eventually it gave up the goods!

![bully_chatbot](https://github.com/jjolley91/blog/blob/main/images/bully_chatbot.png?raw=true)

easy peasy!


#### Confidential Document

> Access a confidential document.

This one had me stumped, However since it specified that the document is supposed to be confidential, I tried logging back in as admin and while clicking around went to the 'About Us' page.

![about_us](https://github.com/jjolley91/blog/blob/main/images/about_us.png?raw=true)
I noticed a link in the txt which downloaded the legal.md document. This did not satisfy the requirement, however. 

Hovering over the link shows: /ftp/legal.md... interesting

![link_address](https://github.com/jjolley91/blog/blob/main/images/link_addr.png?raw=true)

I decided to go to the /ftp directory and sure enough, found a list of some files that looked interesting.

![ftp_directory](https://github.com/jjolley91/blog/blob/main/images/ftp_dir.png?raw=true)

I decided to download the aqusitions.md file and that satisfied the challenge, I also continued poking around here a bit, but decided to move on for now.


#### Error Handling

> Provoke an error that is neither very gracefully nor consistently handled.

There are a bunch of ways to solve this challenge, I just tried another sql login using just a single ' as the username. This breaks the query and causes an error.

![provoke_error](https://github.com/jjolley91/blog/blob/main/images/provoke_error.png?raw=true)


#### Exposed Metrics

>Find the endpoint that serves usage data to be scraped by a [popular monitoring system](https://github.com/prometheus/prometheus).

**Note**: Here there is a hint, as the words 'Popular Monitoring system' are a link.

The link goes to a Github page for Promethus, which seems to be a monitoring system which collects metrics at intervals, triggers alerts, etc..


Eventually after going over the documentation, and trying different directory possibilities, I found the /metrics directory which seems to list processes going on behind the scenes on the site, and also solved this challenge.

![metrics_page](https://github.com/jjolley91/blog/blob/main/images/metrics_page.png?raw=true)

This is referred to as a 'RTFM hack'


#### Mass Dispel

> Close multiple "Challenge solved"-notifications in one go.

For this one, the main challenge was not instantly clicking the 'x' as the notification banner comes up, since you need to have multiple on screen at the same time.

Once you have two or more green banners on your screen, just click the 'x' while holding shift on the keyboard to close all of them at once and solve the challenge!

![mass_dispel](https://github.com/jjolley91/blog/blob/main/images/mass_dispel.png?raw=true)


#### Missing Encoding

> Retrieve the photo of Bjoern's cat in "melee combat-mode"

For this one, since it mentions photos I started with the photo wall, and right away there is a photo that is not loading.

![broken_photo](https://github.com/jjolley91/blog/blob/main/images/broken_photo.png?raw=true)

😼 #zatschi #whoneedsfourlegs

Eventualy I decided to inspect the page and found:

http://10.10.1.5/assets/public/images/uploads/%F0%9F%98%BC-#zatschi-#whoneedsfourlegs-1572600969477.jpg

![broken_photo_inspection](https://github.com/jjolley91/blog/blob/main/images/broken_photo_inspection.png?raw=true)

it seems that the # is causing the HTML to stop reading the address resulting in the photo not being displayed. 

I tried manually urlencoding the # as %23 (which I got from cyberchef) 

![battle_mode](https://github.com/jjolley91/blog/blob/main/images/battle_mode.png?raw=true)

That actually worked and I was graced with a cute cat picture!


#### Outdated Allowlist 

> Let us redirect you to one of our crypto currency addresses which are not promoted any longer.

I ended up back in the main.js in dev tools, searching for 'Redirect'
There were a lot of redirects, but eventually I found one that mentioned blockchain:

![debugger_redirect](https://github.com/jjolley91/blog/blob/main/images/debugger_redirect.png?raw=true)

./redirect?to=https://blockchain.info/address/1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm

http://10.10.1.5/#/redirect?to=https:%2F%2Fblockchain.info%2Faddress%2F1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm

This led me to a wallet with 1.60 balance ( this will be worth more in the future probably)

![btc_wallet](https://github.com/jjolley91/blog/blob/main/images/btc_wallet.png?raw=true)


#### Privacy Policy 

> Read our privacy policy.

This one's easy, just go to account< privacy&security < privacy policy 

![privacy_pol](https://github.com/jjolley91/blog/blob/main/images/priv_pol.png?raw=true)


#### Repetitive Registration 

> Follow the DRY principle while registering a user.

After googling the DRY principle which means Don't Repeat Yourself, I found the only area in the user registration which asks me to repeat myself is the 'Repeat Password' area.

![registration_normal](https://github.com/jjolley91/blog/blob/main/images/registration_normal.png?raw=true)
This was interesting to me, if you type a pw and then mismatch the retype field, the register button is grayed out. However, if you match the passwords and then go and add an extra character to the password field, the register button stayes enabled! Pretty neat!


![registration_broken](https://github.com/jjolley91/blog/blob/main/images/registration_broken.png?raw=true)

Interestingly, the actual password that is saved is the password field, it only checks the Password field and whether or not the retype field matches, but does not check it again after that.


#### Score Board

> Find the carefully hidden 'Score Board' page.

I went over this earlier on in the writeup, to reinterate : I found this by using dev tools to inspect the main.js and search for 'Path:', then look for score-board.


This concludes the level 1 challenges, on to level 2

# Level 2


# Level 3


# Level 4


# Level 5


# Level 6 