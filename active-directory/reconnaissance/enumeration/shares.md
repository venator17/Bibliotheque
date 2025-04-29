---
icon: arrow-up-from-bracket
---

# Shares

## <mark style="color:yellow;">WINDOWS</mark>

<mark style="color:green;">**`NET`**</mark>

```powershell
net share # Check current shares

net view /all /domain[:domainname] # Shares on the domain

net view \computer /ALL # List shares of a computer

net use x: \\computer\share # Mount the share locally
```

### <mark style="color:blue;">Snaffler</mark>

<mark style="color:red;">**Snaffler**</mark> is a tool for <mark style="color:purple;">**finding credentials and sensitive data**</mark> in Active Directory. It scans domain hosts for shared, readable directories and searches for valuable files. It must run from a domain-joined host or a domain-user context. [**\[LINK\]**](https://github.com/SnaffCon/Snaffler)

#### **Snaffler Execution**

```bash
Snaffler.exe -s -d militech.local -o snaffler.log -v data
```

## <mark style="color:yellow;">LINUX</mark>

### <mark style="color:blue;">**CrackMapExec**</mark> <a href="#cme-2" id="cme-2"></a>

**Share Enum**

```bash
sudo crackmapexec smb 13.13.13.13 -u sol -p PASSWORD123 --shares
```

**Spider Share**

```bash
sudo crackmapexec smb 13.13.13.13 -u sol -p PASSWORD123 -M spider_plus --share 'Agent Shares'
```

### <mark style="color:blue;">SMBMap</mark> <a href="#smbmap" id="smbmap"></a>

**Check Access**

```bash
smbmap -u sol -p PASSWORD123 -d MILITECH.LOCAL -H 13.13.13.13
```

**Recursive List of All Dirs**

```bash
smbmap -u sol -p PASSWORD123 -d MILITECH.LOCAL -H 13.13.13.13 -R 'IT Shares' --dir-only
```
