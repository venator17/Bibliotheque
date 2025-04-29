---
icon: user
---

# Users

## <mark style="color:yellow;">WINDOWS</mark>

#### **User Search**

```powershell
PS C:\> dsquery user
```

#### **Checking User Property**

(Property is ServicePrincipalName)

```powershell
PS C:\> Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

#### <mark style="color:green;">`NET`</mark>

```powershell
net user /domain # List all users of the domain

net user <ACCOUNT_NAME> /domain # Get information about a user within the domain

net user %username% # Information about the current user
```

### <mark style="color:blue;">PowerView</mark>

#### **Domain User Information**

```powershell
PS C:\> Get-DomainUser -Identity sol -Domain militech.local | Select-Object -Property name,samaccountname,description,memberof,whencreated,pwdlastset,lastlogontimestamp,accountexpires,admincount,userprincipalname,serviceprincipalname,useraccountcontrol
```

#### **Testing for Local Admin Access**

```powershell
PS C:\> Test-AdminAccess -ComputerName MILITECH-MS13
```

#### **Finding Users With SPN Set**

```powershell
PS C:\> Get-DomainUser -SPN -Properties samaccountname,ServicePrincipalName
```

#### Users with no Password

<pre class="language-powershell"><code class="lang-powershell"><strong>PS C:\> Get-DomainUser -UACFilter PASSWD_NOTREQD | Select-Object samaccountname,useraccountcontrol
</strong></code></pre>

### <mark style="color:blue;">SharpView</mark>

#### **Domain User Information**

```powershell
PS C:\> .\SharpView.exe Get-DomainUser -Identity sol
```

## <mark style="color:yellow;">LINUX</mark>

### <mark style="color:blue;">CrackMapExec</mark> <a href="#cme" id="cme"></a>

#### **CME Domain User** <a href="#cme" id="cme"></a>

```bash
sudo crackmapexec smb 13.13.13.13 -u sol -p PASSWORD123 --users
sudo crackmapexec smb 13.13.13.13 -u sol -p PASSWORD123 --loggedon-users # Logged on
```

### <mark style="color:blue;">RPCClient</mark> <a href="#rpcclient" id="rpcclient"></a>

#### **User Enumeration**

```bash
rpcclient -U "" -N 13.13.13.13 # Get RPC Console
rpcclient $> enumdomusers # Enum all users
rpcclient $> queryuser 0x371 # Enum Specifical User by it's RID
```

### <mark style="color:blue;">Windapsearch</mark> <a href="#windapsearch" id="windapsearch"></a>

[**\[LINK\]**](https://github.com/ropnop/windapsearch)

#### **Domain Admins**

```bash
python3 windapsearch.py --dc-ip 13.13.13.13 -u sol@militech.local -p PASSWORD123 --da
```

#### **Privileged Users**

```bash
python3 windapsearch.py --dc-ip 13.13.13.13 -u sol@militech.local -p PASSWORD123 -PU
```
