---
hidden: true
icon: stairs
---

# Privilege Escalation

## Check setuid root perm's

```bash
find / -user root -perm /4000 2>/dev/null
```
