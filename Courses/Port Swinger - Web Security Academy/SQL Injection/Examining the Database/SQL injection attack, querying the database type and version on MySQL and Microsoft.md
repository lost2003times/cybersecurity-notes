---
topic: SQL injection
level: Practitioner
time_spent: 10 mins
date: 23rd Nov, 2026
---

**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='+UNION+SELECT+@@version,NULL-- #
```

**What I learned:**
We can find out the version information on MySQL and Microsoft as well.

![](SQL%20injection%20attack,%20querying%20the%20database%20type%20and%20version%20on%20MySQL%20and%20Microsoft.md_Attachments/-20261123.png)