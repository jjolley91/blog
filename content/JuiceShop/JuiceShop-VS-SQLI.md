---
title: "JuiceShop vs SQL Injection"
date: 2023-05-25T13:20:30-05:00
tags: ['SQLI','Writeups','JuiceShop', 'SQL Defense and Remediation ']
---
 

 # Intro

 In this blog I will be exploring OWASP Juice Shop using SQL injection techniques, exploring various enumeration methods, and solving the SQL challenges.

Here is a list of challenges I was able to complete using SQL injection. 

### Logging in as Admin:
#### Difficulty: Trivial
### Christmas Special
#### Difficulty: Moderate
### Database Schema
#### Difficulty: Easy
### Retrieving Credentials:
#### Difficulty: Easy
### Login Jim
#### Difficulty: Trivial
### Login Bender
#### Difficulty: Easy
### Ephemeral Accountant
#### Difficulty: Moderate


> NOTE There are also some low hanging fruit challenges that I was able to solve along the way.

### Error Handling
#### Difficulty: Trivial
### Mass Dispel
#### Difficulty: Trivial
### Password Strength
#### Difficulty: Trivial
#### Score-board
#### Difficulty: Trivial
### View Basket
#### Difficulty: Easy

*******************************************************************




The first thing I did was navigate to the login page, and just tried a simple blind sql injection.

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

***************************************************************************

The site uses the /#/ when using search bar or navigating as intended. What comes after the hash(#) is called a fragment. I will not go to deep into why, but essentialy this is just identifying a part of the page, which keeps the query confined to the client side.

For this reason, Trying sql injection directly from the search bar just results in no results found:

![sql_with_hash](https://github.com/jjolley91/blog/blob/main/static/sqli/sql_with_hash.png?raw=true)

So how do we get rid of that pesky hash and get to the good stuff?

The first part of the challenge here is identifying a different way to use the search so that we are able to perform the sql injection.


I used BurpSuite for most of this but I will also note that you can find the same directory by using the devtools < network tab< and searching for 'search'

![dev_tools_method](https://github.com/jjolley91/blog/blob/main/static/sqli/4dev_tools_method.png?raw=true)

>Note: all of the following sql queries can also be done directly from the address bar, but I will be using burp repeater.

First, I fired up BurpSuite, and added the ip address for juice shop to the scope list:

![1_scope](https://github.com/jjolley91/blog/blob/main/static/sqli//1_scope.png?raw=true)

Next, I enabled FoxyProxy and simply refreshed the page to trigger burp to begin mapping the site.

![2site_map](https://github.com/jjolley91/blog/blob/main/static/sqli/2site_map.png?raw=true)

Here you can see the GET request /rest/products/search which I sent to the repeater to start testing for the sql injection potential. Notice here we are not using the hash fragment.

![3send_to_repeater](https://github.com/jjolley91/blog/blob/main/static/sqli/3send_to_repeater.png?raw=true)

Here you can see that with the first attempt, the server returns an error message!

![5first_injection](https://github.com/jjolley91/blog/blob/main/static/sqli/5first_injection.png?raw=true)

This is a very good sign since it tells me that the server is using SQLite, and also that the query did reach the database!

Now I can coninue the injection attack.

>Note: the '; resulted in an error due to the original query not being terminated properly.

Now it is just a matter of determining how many ) were used in the original query.

```SQL
'))--
```

The ')) is used to end the query, and the -- turns the rest of the query into a comment and will be ignored now by the SQL DB.

This does the trick and returns the entire table of products!

![6returned_table](https://github.com/jjolley91/blog/blob/main/static/sqli/6returned_table.png?raw=true)

Since the challenge mentions 'Christmas' I just searched for christmas within the response and noted the ID:10

![7christmas_id](https://github.com/jjolley91/blog/blob/main/static/sqli/7christmas_id.png?raw=true)


Next I went to the site and added an apple to my basket.

I then intercepted the traffic and changed the product id to 10.

![9mod_basket](https://github.com/jjolley91/blog/blob/main/static/sqli/9mod_basket.png?raw=true)

This still did not complete the challenge however, I realized I needed to actually checkout to place the order. Once I did that the challenge was complete!

***************************************************************************

Now that we've found that we can query the database using the /rest/products/search?q=, it is just a matter of querying the database in a way that returns the entire DB schema deffinition. 

Since we know the database is using SQLite, it's simple to google the syntax which that version of sql uses.

We can use the UNION select command to tell the database to perform another search in addition to the one it is already using. 

Since we are querying within the 'Products', it will return an error if the number of columns is not the same.

Use a bit of trial and error to discover the same number of columns as the original query. 

![num_columns](https://github.com/jjolley91/blog/blob/main/static/sqli/num_columns.png?raw=true)

finally, at 9, we have the correct number of columns!

![columns_success](https://github.com/jjolley91/blog/blob/main/static/sqli/columns_success.png?raw=true)

now, we can just replace the first number with sql, and it will return the information for the full database schema in the corresponding column
 
>Note doing this in burp requires you to URL encode the spaces. %20

```HTML
GET /rest/products/search?q=eggs'))UNION%20SELECT%20sql,2,3,4,5,6,7,8,9%20FROM%20sqlite_master--

```

***************************************************************************

#### This section covers the challenges for logging in as Admin, Bender, and Jim.

Now that we know how to get info from the DB, how much info can we get?
The answer is A LOT.

This is just a matter of looking at the fields we got back when we dumped the db schema, and changing the columns to that of the users table:

![sql_user_columns](https://github.com/jjolley91/blog/blob/main/static/sqli/sql_user_columns.png?raw=true)

we can see the list of columns here. Any of these columns look interesting?
>Note: There are more than 9 columns in the users table, but since we are querying through the proudcts search we need to pick nine to use:

![query_users](https://github.com/jjolley91/blog/blob/main/static/sqli/query_users.png?raw=true)

query:
```HTML
 eggs'))UNION%20SELECT%20id,email,password,role,isActive,username,createdAt,deletedAt,totpSecret%20FROM%20Users--
 ```

Note the password field is just under the email field, and they are hashed somehow. I found which type of hash was used by googling for a hash identifier

![id_hash](https://github.com/jjolley91/blog/blob/main/static/sqli/id_hash.png?raw=true)

From here we can retrieve the passwords simply by decrypting the md5 hashes! We can now log in as any user we want!

![hash_decryptor](https://github.com/jjolley91/blog/blob/main/static/sqli/hash_decryptor.png?raw=true)

You can literally log in as any user now, just note the email and decrypt the md5 for the password!

Would you believe there is an even easier way as well? 

Since we know the login page is also vulnerable to sql, and we now have all the emails, we can just craft a query in the login page and just terminate the query after a valid email. No password needed! 

![login_no_pass](https://github.com/jjolley91/blog/blob/main/static/sqli/login_no_pass.png?raw=true)


***************************************************************************

But how can we now login with a user that doesn't already exist?

For this one, I intercepted a bogus login request with burp, and sent it to repeater.

![intercept_request](https://github.com/jjolley91/blog/blob/main/static/sqli/intercept_request.png?raw=true)

we saw the table 'Users' when we dumped the schema, and I also used this method to log in as Bender in the last section. 

But how would we do this when there is no valid account to return as 'true'?

Referring back to the Users information in the database we see that the only thing we need to do here is set the values using 'as'for the information which is missing from the database in order to trick it into evaluating as a valid user:


```SQL

' UNION SELECT * FROM (SELECT 15 as 'id', '' as 'username', 'acc0unt4nt@juice-sh.op' as 'email', '12345' as 'password', 'accounting' as 'role', '123' as 'deluxeToken', '1.2.3.4' as 'lastLoginIp' , '/assets/public/images/uploads/default.svg' as 'profileImage', '' as 'totpSecret', 1 as 'isActive', '1999-08-16 14:14:41.644 +00:00' as 'createdAt', '1999-08-16 14:33:41.930 +00:00' as 'updatedAt', null as 'deletedAt')--
```

That's a pretty beefy query, but it gets the job done! we are now logged in as a nonexistant user!

You can run this command directly from the login screen instead of using burp as well.


Thank you for reading my writeup for SQL injection on Juice Shop. You can check out how to defend against these types of vulnerabilities [here](http://localhost:1313/blog/remediation-and-defense/sql-remediation-and-defense/).