---
icon: tree
---

# Domain

## <mark style="color:yellow;">WINDOWS</mark>

### <mark style="color:blue;">LOL</mark>

#### Display the domain name

```powershell
echo %USERDOMAIN%
```

#### Prints out the name of the Domain controller the host checks in with

```powershell
echo %logonserver%
```

#### Get Domain Info

```powershell
PS C:\> Get-ADDomain
```

#### Computer Search

```powershell
PS C:\> dsquery computer

PS C:\> dsquery * "CN=Users,DC=MILITECH,DC=LOCAL" # Wildcard search
```

#### <mark style="color:green;">`NET`</mark>

```powershell
net accounts # Information about password requirements

net accounts /domain # Password and lockout policy

net view /domain # List of PCs in the domain
```
