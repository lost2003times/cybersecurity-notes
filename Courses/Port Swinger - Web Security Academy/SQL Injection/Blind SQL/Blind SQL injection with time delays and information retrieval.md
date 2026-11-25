---
topic: SQL injection
level: Apprentice
time_spent:
Database type: PostgreSQL
---
**Vulnerability:** 
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

**Payload:**
```
'%3B SELECT CASE WHEN (1=1) 
```

**What I learned:**