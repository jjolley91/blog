---
title: "JuiceShop SQL Defense and Remediation"
date: 2023-05-25T13:20:30-05:00
tags: ['SQLI','Writeups','JuiceShop', 'SQL Defense and Remediation', 'Defense and Remediation']
---

# ![home](https://jjolley91.github.io/blog)

In this writeup I will be discussing Remediation and Defense against SQL injection vulnerabilities based on my [Juice Shop vs SQL injection](https://jjolley91.github.io/blog/juiceshop/juiceshop-vs-sqli/) writeup.

****************************************************************************

Any time there is a search bar, or area a user can imput text on a web application there exists the potential for sql injection. This makes it very important to properly handle queries from any webapp so that someone does not accidentally, or intentionally break your application.

The problem mainly comes from improper configuration.

The solution is to either: not write dynamic queries with string concatenation and/or prevent user supplied input which contains malicious SQL from affecting the intended execution of the query.

As stated above this can be fairly easily remediated with the most effective method being the use of prepared statements with variable binding. 
Prepared statements ensure that someone is not able to use a query in an unintended way. 
All this amounts to is a simple change in the way the query is handled on the backend.

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
This could be used instead:
``` SQL

String custname = request.getParameter("customerName");
// Perform input validation to detect attacks
String query = "SELECT email FROM users WHERE email = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname);
ResultSet results = pstmt.executeQuery( );
```

Another method would be to use Stored Procedures. This simply means that that the SQL code for a stored procedure is defined and stored in the DATABASE , and then called from the application. This is very similar to Prepared Statements. It is also worth noting that even using stored procedures, it is still important to ensure that user inputs are properly sanitized of any escape strings.



Another option would be to use Allow-list input validation. If a user inputs a value that is used for targeting different table names and column names, then the parameter values should be mapped to the legal/expected table or column names to make sure unvalidated user input doesn't end up in the query.


The privileges assigned to the database account should also be limited as much as possible in order to mitigate potential successful SQL injection attacks.


More detailed information for SQL defense and prevention can be found at OWASP's site [here](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)