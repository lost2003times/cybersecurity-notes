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
Cookie: TrackingId=sp6noqfqdKnsOAvQ' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password) > 1) = 'a'--; session=gRAlBYLyISNtGfILsTEgbL9CnCydI2Zg
```

![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/Screenshot%20(63).png)

![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/Screenshot%20(64).png)

![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/Screenshot%20(65).png)

![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/Screenshot%20(66).png)

![](Blind%20SQL%20injection%20with%20conditional%20responses.md_Attachments/Screenshot%20(67).png)

- We used this query to determine the length of the password, and this query is asking the database that is the password of the username = administrator greater than 1 and the 'Welcome back' message is visible but this process will take a lot of time so we use a tool which burp suite offers for such situations.
- We send this request to the intruder and select the LENGTH(password) > ==🔴1==) as our payload and we do the sniper attack on it with the numbers spanning from 1 to 50 with the step 1 so it goes through all the numbers one by one till 50 and we get the welcome back in all the responses till the LENGTH(password) > ==🔴20==), which tells us that the password length is 20.

```
Cookie: TrackingId=sp6noqfqdKnsOAvQ' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator') = 'a'--; session=gRAlBYLyISNtGfILsTEgbL9CnCydI2Zg
```

- Used this query to compare the first letter of the password with 'a' and we can do this for all the letters one by one to figure out the whole password. In SUBSTRING(password,1,1) the the middle 1 is the places of the characters in the password.
- Similarly this can be dealt with the same intruder payload attack we have used earlier.
- So this time there will be 2 payloads which are: (SELECT SUBSTRING(password,==🔴1==,1) and  = '==🔴a=='--
- We set the payload on both of this, and we use Cluster bomb attack on this. Numbers 1 to 20 for the first payload and bruter force for the second payload which goes from a to z to 1 to 0.
- Also we set up grep match to "Welcome back".
- But there is one issue with this kind of an solution that it takes a lot of time as there are around 700 requests to go through and as we have the community version of the burp suite it can take hours.

## Alternate Method 

- We can use binary search tree to tackle the same problem very easily and instead of 700 requests this can be done with around 100 requests.
- So we use ASCII, we know from the hint that the password contains the small letters and the alphanumeric numbers which makes it more easier for us to find it and makes the process even faster.
- We write a python script which contains the UR