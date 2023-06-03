---
title: "JuiceShop vs Broken Access Conrtol"
date: 2023-06-03T13:20:30-05:00
tags: ['Broken Access Control','Writeups','JuiceShop', 'Broken access, Defense and Remediation ']
---
 
# [home](https://jjolley91.github.io/blog)

 # Intro

 In this writeup I will be exploring the Broken Access control of OWASP Juice Shop. 

 Broken access control occurs any time a normal user is able to access restricted or sensitive data.

 ***************************************************************************

Here is a list of challenges I was able to complete using BAC
### Admin Section
#### Difficulty: Easy

### Five-Star Feedback
#### Difficulty: Trivial

### Forged Review
#### Difficulty: Trivial

### Forged Feedback
#### Difficulty: Trivial

### Manipulate Basket
#### Difficulty: Easy

### View Basket
#### Difficulty: Trivial

### Product Tampering
#### Difficulty: Moderate

****************************************************************************

 We can find the administration section by enumerating the directories of the webserver. There are a few different ways to do this:

 The first way is to open the developer tools, and looking in the main.js under debugger, we can search for 'path:' which will take us to a list of the directories.

 ![finding_administration](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/finding_administration.png?raw=true)

 Trying to visit the /administration section gives an error, however if you are not logged in as a user with administrative privileges. 

 ![403_error](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/403_error.png?raw=true)

 So we need to log in as a user with administrative privileges. Let's try making a new user and catching the traffic in Burp to see if we can get some more information.

 ![make_new_user](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/make_new_user.png?raw=true)

 ![request_in_burp](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/request_in_burp.png?raw=true)

 I sent the request to repeater and noticed the response looks a lot like the request, but there are a few extra fields. I tried editing those and it looks like we are able to add the fields we want and become an administrator! 


![add_admin_user](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/add_admin_user.png?raw=true)

Now going back and logging in as the new user, and we are able to visit the administration section!

![admin_section](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/admin_section.png?raw=true)

****************************************************************************
Notice from this page, we are able to see and delete feedback left by customers! 
![delete_5_stars](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/delete_5_stars.png?raw=true)

****************************************************************************

Speaking of feedback, let's go and leave some feedback and see if we can do anything interesting if we catch this request in Burp.

![leaving_feedback](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/leaving_feedback.png?raw=true)

sending the request to repeater, and using the list of users we got from the /administration section, we are easily able to change the author to someone else!

![change_user_feedback](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/change_user_feedback.png?raw=true)

![phony_review](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/phony_review.png?raw=true)

We are able to do the same thing if we go to the customer feedback section:

![cust_feedback](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/cust_feedback.png?raw=true)

Catch the request in burp again, this time we need to change the UserID to any other number:

![mod_feedback](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/mod_feedback.png?raw=true)

****************************************************************************

Lets try adding something to someone else's basket. If we click 'Add to basket', and then move over to burp we see the request:

![our_basket](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/our_basket.png?raw=true)


After some research we can see that if we include our valid basket id first, we are able to append a different basket id to the same request and trick the server into adding the product to another basket! This is called HTTP parameter pollution.

![diff_basket](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/diff_basket.png?raw=true)


****************************************************************************
Moving on, let's see if we can change some items descriptions in the shop. 

First we can see that if we intercept a search request in burp and send to repeater, we get this:

![unmodded_blank_search](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/unmodded_blank_search.png?raw=true)

We can tinker with the request and delete the 'If-None-Match' section and suddenly we get  a list of all the products! 

![modded_request](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/modded_request.png?raw=true)

Now we have the info associated with the "OWASP SSL Advanced Forensic Tool (O-Saft)", next we can attempt to modify it.

After a few attempts we can see that we need to modify the request from:

```HTML
GET /rest/products/search?q= HTTP/1.1
```
We can modify the query to include the product id and change it from /rest/ to /api/

```HTML
GET /api/products/9 HTTP/1.1
```
and we now receive only the product info in our response!

![product_info](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/product_info.png?raw=true)

we can add the description to our request and change it to include the new description by changing the request type from "GET" to "PUT", and adding the Content-Type of application/json.

![changes_to_request_description](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/changes_to_request_description.png?raw=true)


![desc_change_result](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/desc_change_result.png?raw=true)

Now we can change the href link and complete the challenge: 

![final_description](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/final_description.png?raw=true)

****************************************************************************

