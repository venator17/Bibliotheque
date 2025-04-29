# Event Log Readers

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Properly configured**</mark> logging systems is an <mark style="color:purple;">**easy, cheap but very effective**</mark> way to prevent many hacking attempts. as example a lot of hackers after getting into system use commands like: `"`<mark style="color:green;">`whoami, netstat, tasklist, ver, ipconfig, systeminfo, dir, net view, ping, net use, type, at, reg, wmic, wusa`</mark>`"`.  Also logs are usually compatible with a lot of modern <mark style="color:red;">**SIEM (Security Information and Event Management)**</mark> tools.

For hackers logs could be useful for searching sensitive information, like check user logins and find credentials

#### Confirming Membership

```powershell
C:\> net localgroup "Event Log Readers"
```

#### Searching Security Logs

```powershell
PS C:\> wevtutil qe Security /rd:true /f:text | Select-String "/user"
# Do same but from other user
PS C:\> wevtutil qe Security /rd:true /f:text /r:share01 /u:ven17 /p:shrekislove | findstr "/user"
```

#### Searching Logs with `Get-WinEvent`

It's not necessary to be member of **Event Log Readers** group to use this cmdlet. In this command we filter for **process creation events (4688)**, which contain <mark style="color:green;">`/user`</mark> in the process command line.

```powershell
PS C:\> Get-WinEvent -LogName security | where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*'} | Select-Object @{name='CommandLine';expression={ $_.Properties[8].Value }}
```
