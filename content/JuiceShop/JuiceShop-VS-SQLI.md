---
title: "JuiceShop vs SQLI"
date: 2023-05-25T13:20:30-05:00
tags: ['SQLI','Writeups','JuiceShop']
---
 

 # Intro

 In this blog I will be exploring OWASP Juice Shop using SQL injection techniques, exploring various enumeration methods, and solving the SQL challenges.


Any time there is a search bar, or area a user can imput text on a web application there exists the potential for sql injection. This makes it very important to handle all possible edege cases so that someone does not accidentally, or intentionally break your application.

 ### Logging in as Admin using SQL Injection:
 #### Difficulty: Trivial

![sql_login](https://github.com/jjolley91/blog/blob/main/static/sqli/sql_login.png?raw=true)

>email: 'or 1=1--

>password: something



The reason this workes is due to improper imput sanitization before the query is sent to the sql db. Normally the program would be doing something like:

```SQL
SELECT user_id FROM users_table WHERE email_address = 'some@valid.email'  AND password = 'saved_password';
```
However, without being properly handled the query itself can be manipulated so instead of checking if the email is valid and then matching the password in the database, we escaped the query with the single quote, then added a statement which will always evaluate to 'True'. 
We end up with the query:

```SQL
SELECT user_id FROM users_table WHERE email_address = '' OR 1=1--' 

```
Thus we end up canceling the original query and the system just returns the first user in the database, which is usually an admin account! Pretty neat!

### Defense and remediation:

As stated above this can be easily remediated using prepared statements with variable binding. All this amounts to is a simple change in the way the query is handled on the backend.

#### Example:

Instead of something like this vulnerable java example:
``` SQL
String query = "SELECT email FROM users WHERE email = "
             + request.getParameter("customerName");
try {
    Statement statement = connection.createStatement( ... );
    ResultSet results = statement.executeQuery( query );
}
```

``` SQL

String custname = request.getParameter("customerName");
// Perform input validation to detect attacks
String query = "SELECT email FROM users WHERE email = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname);
ResultSet results = pstmt.executeQuery( );
```





### Christmas Special
### Difficulty: Moderate



The site uses the /sqli/#/sqli/search when searching the site from the search bar. What comes after the hash(#) is called a fragment. I will not go to deep into why, but essentialy this is just identifying a part of the page, which keeps the query confined to the client side.

The first part of the challenge here is identifying a different way to use the search so that we are able to perform the sql injection.


I used BurpSuite for most of this but I will also note that you can find the same directory by using the devtools < network tab< and searching for 'search'

![dev_tools_method](https://github.com/jjolley91/blog/blob/main/static/sqli/4dev_tools_method.png?raw=true)

>Note: all of the following sql queries can also be done directly from the address bar, but I will be using burp repeater.

First, I fired up BurpSuite, and added the ip address for juice shop to the scope list:

![1_scope](https://github.com/jjolley91/blog/blob/main/static/sqli//1_scope.png?raw=true)

Next, I enabled FoxyProxy and simply refreshed the page to trigger burp to begin mapping the site.

![2site_map](https://github.com/jjolley91/blog/blob/main/static/sqli/2site_map.png?raw=true)

Here you can see the GET request /sqli/rest/sqli/products/sqli/search which I sent to the repeater to start testing for the sql injection potential.

![3send_to_repeater](https://github.com/jjolley91/blog/blob/main/static/sqli/3send_to_repeater.png?raw=true)

Here you can see that with the first attempt, the server returns an error message!

![5first_injection](https://github.com/jjolley91/blog/blob/main/static/sqli/5first_injection.png?raw=true)

This is a very good sign since it tells me that the server is using SQLite, and also that the query did reach the database!

Now I can coninue the injection attack.

>Note: the '; resulted in an error due to the original query not being ended properly.

To remediate this is just a matter of determining how many ) were used in the original query

```SQL
'))--
```

The ')) is used to end the query, and the -- turns the rest of the query into a comment and will be ignored now by the SQL DB.

This does the trick and returns the entire table of products!

![6returned_table](https://github.com/jjolley91/blog/blob/main/static/sqli/6returned_table.png?raw=true)

Since the challenge mentions 'Christmas' I just searched for christmas within the response and noted the ID:10

![7christmas_id](https://github.com/jjolley91/blog/blob/main/static/sqli/7christmas_id.png?raw=true)

I then intercepted the traffic and changed the product id to 10.

![9mod_basket](https://github.com/jjolley91/blog/blob/main/static/sqli/9mod_basket.png?raw=true)

This still did not complete the challenge however, I realized I needed to actually checkout to place the order. Once I did that the challenge was complete!


### Database Schema
#### Difficulty: Easy

