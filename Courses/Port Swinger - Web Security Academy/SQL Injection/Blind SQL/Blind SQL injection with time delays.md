---
topic: SQL injection
level: Practitioner
time_spent: 15 mins
date: 25th Nov, 2026
Database type: PostgreSQL
---
**Vulnerability:** 
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

**Payload:**
```
Cookie: TrackingId=4ByvR0DrrPDSpakz' || pg_sleep(10)--
```

**What I learned:**
We can add time delays in the request.

![](Blind%20SQL%20injection%20with%20time%20delays.md_Attachments/-20261125.png)

![](Blind%20SQL%20injection%20with%20time%20delays.md_Attachments/-20261125-1.png)

