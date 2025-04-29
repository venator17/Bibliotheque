# DNS

## <mark style="color:yellow;">WINDOWS</mark>

### Resolve DNS

```powershell
PS C:\> Resolve-DnsName DC01.MILITECH.LOCAL
```

## <mark style="color:yellow;">ADIDNSDUMP</mark>

This is tool for DNS Dumping and Enumeration [**\[LINK\]**](https://github.com/dirkjanm/adidnsdump)

```bash
adidnsdump -u militech\\sreed ldap://13.13.13.13 -r
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/recon/dns" %}

{% embed url="https://dirkjanm.io/getting-in-the-zone-dumping-active-directory-dns-with-adidnsdump/" %}
