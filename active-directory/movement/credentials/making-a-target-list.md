# Making a Target List

## <mark style="color:yellow;">Enum4Linux</mark>

```bash
enum4linux -U 13.13.13.13 | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
```

## <mark style="color:yellow;">RPCClient</mark>

```bash
rpcclient -U "" -N 13.13.13.13
rpcclient $> enumdomusers
```

## <mark style="color:yellow;">CrackMapExec</mark>

```bash
crackmapexec smb 13.13.13.13 --users
```

## <mark style="color:yellow;">LDAPSearch</mark>

```bash
ldapsearch -h 13.13.13.13 -x -b "DC=MILITECH,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "
```

## <mark style="color:yellow;">WindapSearch</mark>

```bash
./windapsearch.py --dc-ip 13.13.13.13 -u "" -U
```

## <mark style="color:yellow;">Kerbrute</mark>

```bash
kerbrute userenum -d militech.local --dc 13.13.13.13 /opt/jsmith.txt 
```

## <mark style="color:yellow;">Linkedin2Username</mark>

Useful tool to generate a userlist from Linkedin [**\[LINK\]**](https://github.com/initstring/linkedin2username)

```bash
python linkedin2username.py -c targetco
```

## <mark style="color:yellow;">Credentialed CME</mark>

```bash
sudo crackmapexec smb 13.13.13.13 -u sreed -p pwd123 --users
```
