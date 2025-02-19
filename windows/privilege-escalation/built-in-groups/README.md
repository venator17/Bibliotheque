# Built-In Groups

## <mark style="color:yellow;">About</mark>

<mark style="color:red;">**Windows servers**</mark>, and especially <mark style="color:red;">**Domain Controllers**</mark>, <mark style="color:purple;">**have a variety of built-in groups**</mark> that either ship with the operating system or get added when the Active Directory Domain Services role is installed on a system to promote a server to a Domain Controller. Many of these groups confer <mark style="color:orange;">**special privileges**</mark> on their members, and some can be leveraged to escalate privileges on a server or a Domain Controller

## <mark style="color:yellow;">Checking Group Membership</mark>

```powershell
whoami /groups
```
