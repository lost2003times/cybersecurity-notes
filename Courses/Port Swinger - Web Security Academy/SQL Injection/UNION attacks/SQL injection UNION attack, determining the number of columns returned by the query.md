---
topic: SQL injection
level: Practitioner
time_spent: 10 mins
date: 22 Nov, 2026
---

**Vulnerability:** 
SQL injection vulnerability in the product category filter

**Payload:**
```
categoty='+UNION+SELECT+NULL,NULL,NULL--
```

**What I learned:**
By using the UNION I added another SELECT query where I found out the columns using NULL because it is comparable to almost all the data types which makes it easier to find out the number of columns.
UNION has 2 requirements to work which are : 
- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.