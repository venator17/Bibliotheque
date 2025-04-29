# AddMember

## <mark style="color:yellow;">Check membership</mark>

```powershell
PS C:\> Get-ADGroup -Identity "NC Agents" -Properties * | Select -ExpandProperty Members
```

## <mark style="color:yellow;">Adding user to group</mark>

<mark style="color:orange;">**PowerView Required!**</mark>

```powershell
PS C:\> Add-DomainGroupMember -Identity 'NC Agents' -Members 'songbird' -Credential $Cred -Verbose
```

## <mark style="color:yellow;">Deleting user from group</mark>

```powershell
PS C:\> Remove-DomainGroupMember -Identity "NC Agents" -Members 'songbird' -Credential $Cred -Verbose
```

