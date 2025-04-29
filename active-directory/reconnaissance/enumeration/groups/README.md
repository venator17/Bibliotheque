---
icon: people-group
---

# Groups

## <mark style="color:yellow;">WINDOWS</mark>

#### **Detailed Group Info**

```powershell
PS C:\> Get-ADGroup -Identity "Backup Operators"
```

#### Group Membership

```powershell
PS C:\> Get-ADGroupMember -Identity "Backup Operators"
```

#### <mark style="color:green;">**`NET`**</mark>

```powershell
net localgroup administrators /domain # List users in the administrators group inside the domain

net group /domain # Information about domain groups

net groups /domain # List of domain groups

net group <domain_group_name> /domain # Users belonging to the group

net group "Domain Admins" /domain # List users with domain admin privileges

net group "Domain Controllers" /domain # List PC accounts of domain controllers

net group "domain computers" /domain # List of PCs connected to the domain
```

#### Get Group SID

```powershell
C:\> Get-ADGroup -Identity "Enterprise Admins" -Server "MILITECH.LOCAL
```

### <mark style="color:blue;">PowerView</mark>

#### **Recursive Group Membership**

```powershell
PS C:\>  Get-DomainGroupMember -Identity "Domain Admins" -Recurse
```

#### Check RDP Users Group

```powershell
PS C:\> Get-NetLocalGroupMember -ComputerName MILITECH-MS13 -GroupName "Remote Desktop Users"
```

#### Check Remote Management Users Group

```powershell
PS C:\> Get-NetLocalGroupMember -ComputerName MILITECH-MS13 -GroupName "Remote Management Users"
```

#### Check Foreign Group Membership

<pre class="language-powershell"><code class="lang-powershell"><strong>PS C:\> Get-DomainForeignGroupMember -Domain MILITECH.LOCAL
</strong></code></pre>

#### Get Group's SID

```powershell
PS C:\> Get-DomainGroup -Domain MILITECH.LOCAL -Identity "Enterprise Admins" | select distinguishedname,objectsid
```

## <mark style="color:yellow;">LINUX</mark>

### <mark style="color:blue;">CrackMapExec</mark> <a href="#cme-1" id="cme-1"></a>

#### **Groups**

```bash
sudo crackmapexec smb 13.13.13.13 -u sreed -p PASSWORD123 --groups
```
