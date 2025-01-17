---
icon: lock-keyhole
---

# Security

## <mark style="color:yellow;">ABOUT</mark>

Here I would write about <mark style="color:purple;">**security mechanisms**</mark> in Windows. Since Windows theory is very broad, and to avoid making the theory page bloated, I would write here about the security side of Windows

## <mark style="color:yellow;">AUTHENTICATION PROCESS</mark>

<figure><img src="../../.gitbook/assets/win_authproc_image.png" alt=""><figcaption></figcaption></figure>

## <mark style="color:yellow;">SAM</mark>

<mark style="color:red;">**The Security Accounts Manager**</mark>**&#x20;is a&#x20;**<mark style="color:purple;">**database file**</mark>**&#x20;in the Microsoft Windows operating system that contains usernames and passwords.** The SAM is available in different versions of Windows, including XP, Vista, 7, 8.1, 10 and 11. Each user account can be assigned a local area network (LAN) and a password would be hashed and stored in the SAM. The passwords hashes are stored in <mark style="color:green;">**HKEY\_LOCAL\_MACHINE\SAM**</mark><mark style="color:blue;">**,**</mark> but the access to it is restricted. **HKLM/SAM** and **SYSTEM** privileges are required for accessing it.

## <mark style="color:yellow;">SID</mark>

<mark style="color:red;">**Security Identifier (SID)**</mark> is <mark style="color:purple;">**unique, system-generated identifier**</mark> for each security principal on a system. Even identical users are distinguished by their SIDs, which determine their permissions. SIDs are stored in the security database and included in access tokens to manage user actions.&#x20;

A SID consists of the <mark style="color:red;">**Identifier Authority**</mark> and the <mark style="color:red;">**Relative ID (RID)**</mark>. In an **Active Directory (AD)** domain environment, the SID also includes the domain SID.

#### SID Structure:

<mark style="color:green;">`(SID)-(revision level)-(identifier-authority)-(subauthority1)-(subauthority2)-(etc)`</mark>

<mark style="color:green;">`S-1-5-21-674899381-4069889467-2080702030-1002`</mark>

| **Number**                                         | **Meaning**              | **Description**                                                               |
| -------------------------------------------------- | ------------------------ | ----------------------------------------------------------------------------- |
| <mark style="color:blue;">**S**</mark>             | **SID**                  | Indicates the string is a SID.                                                |
| <mark style="color:blue;">**1**</mark>             | **Revision Level**       | Always 1, showing the SID format version.                                     |
| <mark style="color:blue;">**5**</mark>             | **Identifier Authority** | Identifies the authority (e.g., computer or network) that created the SID.    |
| <mark style="color:blue;">**21**</mark>            | **Subauthority 1**       | Shows the user's relation or group to the authority that created the SID.     |
| <mark style="color:blue;">**674899381-...**</mark> | **Subauthority 2**       | Identifies the specific computer or domain that created the SID.              |
| <mark style="color:blue;">**1002**</mark>          | **Subauthority 3 (RID)** | Differentiates accounts, indicating roles like user, guest, or administrator. |

## <mark style="color:yellow;">LSASS</mark>

<mark style="color:red;">**Local Security Authority Subsystem Service (LSASS)**</mark> is a <mark style="color:purple;">**collection of many modules**</mark> and has access to all authentication processes that can be found in <mark style="color:green;">`%SystemRoot%\System32\Lsass.exe`</mark>. <mark style="color:green;">**`lsass.exe`**</mark> is the <mark style="color:purple;">**process**</mark> that is responsible for **enforcing the security policy on Windows systems**.&#x20;

When a user attempts to log on to the system, this process verifies their log on attempt and creates access tokens based on the user's permission levels. LSASS is also responsible for <mark style="color:yellow;">**user account password changes**</mark>.&#x20;

All events associated with this process (logon/logoff attempts, etc.) are logged within the **Windows Security Log**. <mark style="color:orange;">**LSASS is an extremely high-value target**</mark> as several tools exist to extract both cleartext and hashed credentials stored in memory by this process.

### <mark style="color:blue;">LSA Secrets</mark>

**LSA Secrets** are <mark style="color:purple;">**sensitive data**</mark> stored by the **Local Security Authority** (LSA) on Windows systems. Key Types of LSASS Secrets are:

1. <mark style="color:orange;">**Hashes**</mark>\
   LSASS stores password hashes for logged-in users. These can be used in attacks like **Pass-the-Hash** to authenticate without knowing the plain-text password.
2. <mark style="color:orange;">**Kerberos Tickets**</mark>\
   LSASS holds Kerberos tickets (TGTs and service tickets) used in Active Directory environments to authenticate users across the network.
3. <mark style="color:orange;">**Plain-Text Passwords**</mark>\
   In some cases, LSASS may store plain-text passwords or reversible encryption keys for convenience in single sign-on (SSO) scenarios.
4. <mark style="color:orange;">**Security Tokens**</mark>\
   LSASS maintains security tokens that represent a user’s session and define what resources the user can access.

This data is stored in the Windows Registry at <mark style="color:green;">**`HKEY_LOCAL_MACHINE\Security\Policy\Secrets`**</mark>

## <mark style="color:yellow;">ACL</mark>

<figure><img src="../../.gitbook/assets/ACL SCHEME.png" alt="" width="563"><figcaption><p><strong>ACL Structure</strong></p></figcaption></figure>

<mark style="color:red;">**Access Control List (ACL)**</mark> is a <mark style="color:purple;">**list of rules**</mark> that specifies which users or groups are allowed to access an object, such as a file or folder, and what actions they can perform (e.g., read, write, or execute).

<mark style="color:red;">**Discretionary Access Control List (DACL)**</mark> is a type of ACL that <mark style="color:purple;">**defines the permissions for users and groups to access an object**</mark>. It controls what actions can be performed on the object by each user or group, and the owner of the object can modify the DACL.

<mark style="color:red;">**System Access Control List (SACL)**</mark>, on the other hand, <mark style="color:purple;">**specifies what events related to an object should be logged for auditing purposes**</mark>. It helps track access attempts, whether successful or not.

<mark style="color:red;">**Access Control Entry (ACE)**</mark> is an <mark style="color:purple;">**individual entry in an ACL**</mark> that defines which users, groups, or processes have access to a file or to execute a process, for example. Each ACE lists the access rights granted or denied to a principal (user or group).

## <mark style="color:yellow;">UAC</mark>

<mark style="color:red;">**User Account Control (UAC)**</mark> is a <mark style="color:purple;">**security feature**</mark> in Windows to **prevent malware from running or manipulating processes** that could damage the computer or its contents.&#x20;

There is the Admin Approval Mode in UAC, which is designed to prevent unwanted software from being installed without the administrator's knowledge or to prevent system-wide changes from being made.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p><strong>UAC Strucure</strong> <a href="https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works"><strong>[SOURCE]</strong></a></p></figcaption></figure>

## <mark style="color:yellow;">NTLM</mark>
