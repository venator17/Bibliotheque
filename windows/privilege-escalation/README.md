---
icon: stairs
---

# Privilege Escalation

The general goal of <mark style="color:red;">**Windows privilege escalation**</mark> is to <mark style="color:purple;">**further our access to a given system**</mark> to a member of the **Local Administrators** group or the <mark style="color:green;">`NT AUTHORITY\SYSTEM`</mark> LocalSystem account. There may, however, be scenarios where escalating to another user on the system may be enough to reach our goal. Privilege escalation is often vital to continue through a network towards our ultimate objective, as well as for lateral movement.

As penetration testers, it's vital to understand **manual privilege escalation techniques**, especially in restrictive environments. When placed on a managed workstation with no internet, strict firewalls, and disabled USB ports, relying solely on tools or scripts may not be an option. In such cases, mastering Windows privilege escalation checks via PowerShell and the command line is essential.

Some of the ways that we can escalate privileges are:

* **Abusing Windows group privileges**&#x20;
* **Abusing Windows user privileges**&#x20;
* **Bypassing User Account Control**&#x20;
* **Abusing weak service/file permissions**&#x20;
* **Leveraging unpatched kernel exploits**&#x20;
* **Credential theft**&#x20;
* **Traffic Capture**
