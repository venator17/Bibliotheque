---
description: >-
  For now don't know any methods from enumerating ACL's from Linux except
  BloodHound and PowerView, so yeah. No Windows / Linux sections here.
icon: list-check
---

# ACL

## <mark style="color:yellow;">PowerView</mark>

```powershell
PS C:\> Import-Module .\PowerView.ps1
```

### <mark style="color:blue;">Object</mark>

#### Get Info About an AD Object

```powershell
PS C:\> $sid = Convert-NameToSid sreed
PS C:\> Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $sid} -Verbose
```

This commands works like this. In <mark style="color:blue;">`$sid`</mark> we put sid of an object we want to know more about (doesn't matter if this user or group).&#x20;

* <mark style="color:green;">`Get-DomainObjectACL - Identity *`</mark> retrieves all ACL's about all objects in AD. But we pipe this to command which filters our user mention to get info about ACL's related to our object.&#x20;
* <mark style="color:green;">`-ResolveGUIDs`</mark> parameter is for explaining what this GUID stands for.

### <mark style="color:blue;">Users</mark>

#### Dump all AD usernames into a file

```powershell
PS C:\> Get-ADUser -Filter * | Select-Object -ExpandProperty SamAccountName > ad_users.txt
```

#### **Which users OUR user has access over**

```powershell
PS C:\> foreach($line in [System.IO.File]::ReadLines("C:\Path\To\ad_users.txt")) {get-acl  "AD:\$(Get-ADUser $line)" | Select-Object Path -ExpandProperty Access | Where-Object {$_.IdentityReference -match 'MILITECH\\sreed'}}
```

### <mark style="color:blue;">Groups</mark>

#### Check Nested Groups

```powershell
PS C:\> Get-DomainGroup -Identity "group" | select memberof
```

### <mark style="color:blue;">GUID</mark>

#### Resolve GUID to human-readable permission name

```powershell
PS C:\> $guid= "00299570-246d-11d0-a768-00aa006e0529"
PS C:\> Get-ADObject -SearchBase "CN=Extended-Rights,$((Get-ADRootDSE).ConfigurationNamingContext)" -Filter {ObjectClass -like 'ControlAccessRight'} -Properties * |Select Name,DisplayName,DistinguishedName,rightsGuid| ?{$_.rightsGuid -eq $guid} | fl
```
