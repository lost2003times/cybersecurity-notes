---
topic: SQL injection
level: Practitioner
time_spent: 10 mins
date: 22 Nov, 2026
---
Retrieving Interesting data and using it to login.

**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='+UNION+SELECT+username,+password+FROM+users--
```

**What I learned:**
After determining the columns and the data type it contains we can use UNION to retrieve data like usernames and passwords as well and use that information to login.