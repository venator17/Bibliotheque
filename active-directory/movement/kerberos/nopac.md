# noPAC

## <mark style="color:yellow;">ABOUT</mark>

Novemer 2021, it was discovered that combination of two vulnerabilities could allow domain escalation from a standart user.

### <mark style="color:blue;">CVE-2021-42278</mark>

Name Impersonation vulnerability. Was caused because of absence of checking `$` after computer account name (because of sAMAccountName attribute).

### <mark style="color:blue;">CVE-2021-42287</mark>

When requesting a ST, you should present a TGT. When ST is not found by KDC, it searches again with `$`. So imagine if we found TGT for user `bob`, then `bob` gets deleted, so it searches for `bob$`. If it exists, we could obtain ST for `bob$`.

### <mark style="color:blue;">Prerequisites</mark>

* Authenticated low-privileged AD user
* Unpatched DC vulnerable to both CVEs
* Attacker can create machine accounts (default: 10 per user)

## <mark style="color:yellow;">FLOW</mark>

1. Make / Rename pc account with similar name to DC but with $
2. Ask for TGT for this user
3. Delete / Change back name of pc account
4. Use that TGT to request for TGS
5. TGS checks who ownes that TGT. Checks original name, empty (Cause we deleted/changed name). so it tries same name but with $
6. Success, KDC thinks that you're TGT is DC's TGT

## <mark style="color:yellow;">LINUX</mark>

For executing this vuln from Linux we need this exploit: [**\[LINK\]**](https://github.com/Ridter/noPac)

#### Scanning for noPAC

```shell-session
sudo python3 scanner.py militech.local/sreed:passsword123 -dc-ip 13.13.13.13 -use-ldap
```

#### Running noPAC & Shell

```shell-session
sudo python3 noPac.py MILITECH.LOCAL/sreed:password123 -dc-ip 13.13.13.13 -dc-host MILITECH-EA-DC01 -shell --impersonate administrator -use-ldap
```

> Session would be made with impacket's smbexec

> Also noPAC would save TGT in local directory

#### DCSync using noPAC

```shell-session
sudo python3 noPac.py MILITECH.LOCAL/sreed:password123 -dc-ip 13.13.13.13  -dc-host MILITECH-EA-DC01 --impersonate administrator -use-ldap -dump -just-dc-user MILITECH/administrator
```

> Basically we just changed <mark style="color:green;">`-shell`</mark>l parameter with <mark style="color:green;">`-dump`</mark>

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/movement/kerberos/samaccountname-spoofing#machine-account" %}
