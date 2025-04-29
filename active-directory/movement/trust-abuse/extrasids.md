# ExtraSIDs

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**ExtraSIDs**</mark> is a technique where a forged Kerberos ticket <mark style="color:yellow;">**(Golden Ticket) includes additional SIDs**</mark>, typically from a more privileged domain like the parent domain in a forest, allowing an attacker who compromised a child domain to impersonate membership in high-privilege groups such as Enterprise Admins and gain unauthorized access across domain boundaries, bypassing normal group membership checks if SID filtering is not enforced.

### <mark style="color:blue;">Prerequisites</mark>

## <mark style="color:yellow;">LINUX</mark>

#### Bruteforce SID

```bash
impacket-lookupsid fia.militech.local/sreed@13.13.13.13 | grep "Enterprise Admins"
```

## <mark style="color:yellow;">WINDOWS</mark>

#### Get Group SID

```powershell
C:\> Get-ADGroup -Identity "Enterprise Admins" -Server "MILITECH.LOCAL"
```

### <mark style="color:blue;">PowerView</mark>

#### Get Group SID

```powershell
PS C:\> Get-DomainGroup -Domain MILITECH.LOCAL -Identity "Enterprise Admins" | select distinguishedname,objectsid
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://learn.microsoft.com/en-us/windows/win32/adschema/a-sidhistory" %}
