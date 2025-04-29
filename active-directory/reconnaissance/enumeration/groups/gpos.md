# GPO's

## <mark style="color:yellow;">WINDOWS</mark>

#### Enum GPO's Names

```powershell
PS C:\> Get-GPO -All | Select DisplayName
```

#### Convert GPO GUID to Name

```powershell
PS C:\> Get-GPO -Guid 7CA91239-14CE-4137-A622-83123127AF532
```

### <mark style="color:blue;">PowerView</mark>

#### Enum GPO's Names

```powershell
PS C:\> Get-DomainGPO |select displayname
```

#### **Enumerating Domain User GPO Rights**

```powershell
PS C:\> $sid=Convert-NameToSid "Domain Users"
PS C:\> Get-DomainGPO | Get-ObjectAcl | ?{$_.SecurityIdentifier -eq $sid}
```

