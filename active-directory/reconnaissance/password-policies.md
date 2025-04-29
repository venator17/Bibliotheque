# Password Policies

## <mark style="color:yellow;">FROM LINUX</mark>

### <mark style="color:blue;">CrackMapExec:</mark>

<mark style="color:yellow;">**With valid domain credentials**</mark>, the password policy can be obtained remotely using tools like <mark style="color:green;">**`CrackMapExec`**</mark> or <mark style="color:green;">**`rpcclient`**</mark>.

```bash
crackmapexec smb 13.13.13.13 -u sol -p pwd123 --pass-pol
```

### <mark style="color:blue;">SMB NULL Sessions</mark>

An SMB NULL session may allow an attacker to retrieve domain information <mark style="color:yellow;">**without authentication.**</mark>

#### Using rpcclient:

```bash
rpcclient -U "" -N 13.13.13.13
rpcclient $> querydominfo
rpcclient $> getdompwinfo
```

#### Using enum4linux:

```bash
enum4linux -P 13.13.13.13
```

#### Using enum4linux-ng:

```bash
enum4linux-ng -P 13.13.13.13 -oA militech
cat militech.json
```

### <mark style="color:blue;">LDAP Anonymous Bind</mark>

#### Using ldapsearch:

```bash
ldapsearch -h 13.13.13.13 -x -b "DC=ARASAKA,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```

## <mark style="color:yellow;">FROM WINDOWS</mark>

### <mark style="color:blue;">**net.exe**</mark>

```powershell
C:\> net accounts
```

### <mark style="color:blue;">**PowerView**</mark>

```powershell
PS C:\> import-module .\PowerView.ps1
PS C:\> Get-DomainPolicy
```
