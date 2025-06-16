---
icon: paw-simple
---

# Kerberos

## <mark style="color:yellow;">THEORY</mark>

{% embed url="https://venator17.gitbook.io/bibliotheque/active-directory/theory#kerberos" %}

## CLOCK ERROR

> `[-] Got error while trying to request TGT: Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great)`

It's very common (at least in HTB Boxes) error because of time zone difference timestamp header in authentication packets is getting to big. So the fix is time sync with server

#### Stop default automatic time sync

```bash
sudo systemctl stop systemd-timesyncd
```

#### Sync time with server

```bash
sudo ntpdate 13.13.13.13
```

#### Change time back

```bash
timedatectl set-ntp 1
```
