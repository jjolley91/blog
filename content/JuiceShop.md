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


![sql_login](sqlimg.png)

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

![admin_email](admin_email.png)


OK, Still just poking around on my own I eventually clicked on the 'Help getting started' which gave a pop-up with a few interesting hints such as:

>You find the JavaScript code in the DevTools of your browser that will open with F12.
		
>Look through the client-side JavaScript in the Sources tab for clues. Or just start URL guessing. It's up to you!

>This application is riddled with security vulnerabilities. Your progress exploiting these is tracked on a Score Board.

>You won't find a link to it in the navigation or side bar, though. Finding the Score Board is in itself actually one of the hacking challenges.


I looked in Dev tools< Debugger (right click the screen, then choose inspect) and searched (ctrl+f) for 'Score'  which gave me:

```js
path: 'score-board'
```
![debugger_search](debugger_search.png)


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

![score-board-page](scoreboard_page.png)


By this point it shows I have completed 1 level 1 challenge and one level 2 challenge, but from here on I will attempt to solve these in the order they appear by difficulty.

# Level  1


### Challenge name




# Level 2


# Level 3


# Level 4


# Level 5


# Level 6 