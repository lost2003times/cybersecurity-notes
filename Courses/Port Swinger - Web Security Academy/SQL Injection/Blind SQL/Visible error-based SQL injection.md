---
topic: SQL injection
level: Apprentice
time_spent: 20 mins
date: 24th Nov,2026
---

**Vulnerability:** 
This lab contains a SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned.

**Payload:**
```
TrackingId =' AND CAST((SELECT 1) as int)--
```

- With this we get the error that the 
**What I learned:**