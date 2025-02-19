---
icon: certificate
---

# Privileges

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**Privileges**</mark> in Windows are <mark style="color:purple;">**rights that an account can be granted to perform a variety of operations**</mark>**&#x20;on the local system such as managing services, loading drivers, shutting down the system, debugging an application, and more**.&#x20;

Privileges are different from access rights, which a system uses to grant or deny access to securable objects. User and group privileges are stored in a database and granted via an access token when a user logs on to a system. An account can have local privileges on a specific computer and different privileges on different systems if the account belongs to an Active Directory domain. Each time a user attempts to perform a privileged action, the system reviews the user's access token to see if the account has the required privileges, and if so, checks to see if they are enabled. Most privileges are disabled by default. Some can be enabled by opening an administrative cmd.exe or PowerShell console, while others can be enabled manually.

When a privilege is listed for our account in the <mark style="color:blue;">`Disabled`</mark> state, it means that our account has the specific privilege assigned. Still, it cannot be used in an access token to perform the associated actions until it is enabled.

## <mark style="color:yellow;">Enable Privilege</mark>

**Enable All Token Privs** [**\[LINK\]**](https://raw.githubusercontent.com/fashionproof/EnableAllTokenPrivs/master/EnableAllTokenPrivs.ps1)

```powershell
PS C:\> Import-Module .\Enable-Privilege.ps1
PS C:\> .\EnableAllTokenPrivs.ps1
```

## <mark style="color:yellow;">Key Groups</mark>

| **Group**                                                        | **Description**                                                                                     |
| ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| <mark style="color:blue;">**Default Administrators**</mark>      | Domain Admins and Enterprise Admins with unrestricted privileges.                                   |
| <mark style="color:blue;">**Server Operators**</mark>            | Modify services, access SMB shares, backup files.                                                   |
| <mark style="color:blue;">**Backup Operators**</mark>            | Log onto Domain Controllers (DCs), backup SAM/NTDS database, and access the DC file system via SMB. |
| <mark style="color:blue;">**Print Operators**</mark>             | Log onto DCs and potentially load malicious drivers.                                                |
| <mark style="color:blue;">**Hyper-V Administrators**</mark>      | Manage virtual DCs and should be considered equivalent to Domain Admins.                            |
| <mark style="color:blue;">**Account Operators**</mark>           | Modify non-protected accounts and groups in the domain.                                             |
| <mark style="color:blue;">**Remote Desktop Users**</mark>        | Typically used for lateral movement via Remote Desktop Protocol (RDP).                              |
| <mark style="color:blue;">**Remote Management Users**</mark>     | Log on to DCs using PowerShell Remoting.                                                            |
| <mark style="color:blue;">**Group Policy Creator Owners**</mark> | Create new GPOs but need delegated permissions to link them.                                        |
| <mark style="color:blue;">**Schema Admins**</mark>               | Modify the AD schema structure and insert backdoors into new GPOs.                                  |
| <mark style="color:blue;">**DNS Admins**</mark>                  | Can load malicious DLLs on DCs for persistence but cannot restart the DNS service.                  |

## <mark style="color:yellow;">Common User Rights Assignments:</mark>

| **Constant**                                                     | **Setting Name**                         | **Standard Assignment**              | **Description**                                                |
| ---------------------------------------------------------------- | ---------------------------------------- | ------------------------------------ | -------------------------------------------------------------- |
| <mark style="color:blue;">`SeNetworkLogonRight`</mark>           | Access this computer from the network    | Administrators, Authenticated Users  | Allows connecting to a system over the network.                |
| <mark style="color:blue;">`SeRemoteInteractiveLogonRight`</mark> | Allow log on via Remote Desktop Services | Administrators, Remote Desktop Users | Enables remote desktop access.                                 |
| <mark style="color:blue;">`SeBackupPrivilege`</mark>             | Back up files and directories            | Administrators                       | Overrides permissions to back up system data.                  |
| <mark style="color:blue;">`SeTakeOwnershipPrivilege`</mark>      | Take ownership of objects                | Administrators                       | Assign ownership of NTFS objects, registry keys, etc.          |
| <mark style="color:blue;">`SeDebugPrivilege`</mark>              | Debug programs                           | Administrators                       | Attach to or debug processes, even those owned by other users. |
| <mark style="color:blue;">`SeImpersonatePrivilege`</mark>        | Impersonate a client                     | Administrators, Service accounts     | Act on behalf of another user after authentication.            |
| <mark style="color:blue;">`SeRestorePrivilege`</mark>            | Restore files and directories            | Administrators                       | Bypass permissions for restoring system data.                  |
