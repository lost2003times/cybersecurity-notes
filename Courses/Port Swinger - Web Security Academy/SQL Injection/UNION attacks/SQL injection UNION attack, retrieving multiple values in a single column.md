---
topic: SQL injection
level: Practitioner
time_spent: 15 mins
date: 22 Nov, 2026
---

**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

**What I learned:**
Both the columns did not contain the string type data so we concatenated both the username and password data into one column separating both the strings data with '~' so we received the username and password from the users table.
We can write anything ||'anything'|| here instead of ||'~'||.
