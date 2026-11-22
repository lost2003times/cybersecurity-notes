---
topic: SQL injection
level: Practitioner
time_spent: 10 mins
date: 22nd Nov, 2026
---

**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='+UNION+SELECT+NULL,'Jayman',NULL--
```

**What I learned:**
After determining the number of columns I was able to pass on the string determining that the columns contains strings as data.