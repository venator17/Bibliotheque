---
icon: redhat
---

# Techniques

## <mark style="color:yellow;">**Check available network interfaces**</mark>

```bash
iwconfig
OR
ss -tulpn #(or тюльпан for remembering)
OR
netstat -tulpn
```

## <mark style="color:yellow;">Ping Scan</mark>

```bash
for i in {1..255} ;do (ping -c 1 13.13.13.$i | grep "bytes from"|cut -d ' ' -f4|tr -d ':' &);done
```

