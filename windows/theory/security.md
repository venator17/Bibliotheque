---
icon: lock-keyhole
---

# Security

## <mark style="color:yellow;">ABOUT</mark>

Here I would write about <mark style="color:purple;">**security mechanisms**</mark> in Windows. Since Windows theory is very broad, and to avoid making the theory page bloated, I would write here about the security side of Windows.&#x20;

## <mark style="color:yellow;">AUTHENTICATION</mark>

<mark style="color:red;">**Authentication**</mark> is process of verifying <mark style="color:purple;">**who someone is.**</mark>

<figure><img src="../../.gitbook/assets/win_authproc_image.png" alt=""><figcaption></figcaption></figure>

## <mark style="color:yellow;">AUTHORIZATION</mark>

<mark style="color:red;">**Authorization**</mark> is process of determining <mark style="color:purple;">**what someone is allowed to do**</mark><mark style="color:purple;">.</mark>

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p><a href="https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-principals"><strong>[SOURCE]</strong></a></p></figcaption></figure>

<mark style="color:red;">**Security principals**</mark> are <mark style="color:purple;">**anything that can be authenticated**</mark> by the Windows operating system, including user and computer accounts, processes that run in the security context or another user/computer account, or the security groups that these accounts belong to. Every single security principal is identified by a unique <mark style="color:red;">**Security Identifier (SID)**</mark>. When a security principal is created, it is assigned a SID which remains assigned to that principal for its lifetime.

1. <mark style="color:blue;">**User Authentication and Access Token Generation.**</mark> A user logs into the system or attempts to access a resource. The system authenticates the user and generates an **access token**.
2. <mark style="color:blue;">**Request to Access a Securable Object.**</mark> The user attempts to access a **securable object**. The object has a **security descriptor** that includes its **Access Control List (ACL)**. The ACL contains **Access Control Entries (ACEs)**, which define which SIDs (users or groups) have specific permissions to access the object.
3. <mark style="color:blue;">**Comparison of Access Token and Security Descriptor.**</mark> The system compares the user's **access token** (SIDs and privileges) with the object's **ACEs** in the security descriptor. Permissions such as **Read**, **Write**, **Execute**, etc., are checked against the ACEs to determine whether the user has the required access rights.
4. <mark style="color:blue;">**Access Decision.**</mark>

## <mark style="color:yellow;">SAM</mark>

<mark style="color:red;">**The Security Accounts Manager**</mark>**&#x20;is a&#x20;**<mark style="color:purple;">**database file**</mark>**&#x20;in the Microsoft Windows operating system that contains usernames and passwords.** The SAM is available in different versions of Windows, including XP, Vista, 7, 8.1, 10 and 11. Each user account can be assigned a local area network (LAN) and a password would be hashed and stored in the SAM. The passwords hashes are stored in <mark style="color:green;">**HKEY\_LOCAL\_MACHINE\SAM**</mark><mark style="color:blue;">**,**</mark> but the access to it is restricted. **HKLM/SAM** and **SYSTEM** privileges are required for accessing it.

## <mark style="color:yellow;">SID</mark>

<mark style="color:red;">**Security Identifier (SID)**</mark> is <mark style="color:purple;">**unique, system-generated identifier**</mark> for each security principal on a system. Even identical users are distinguished by their SIDs, which determine their permissions. SIDs are stored in the security database and included in access tokens to manage user actions.&#x20;

A SID consists of the <mark style="color:red;">**Identifier Authority**</mark> and the <mark style="color:red;">**Relative ID (RID)**</mark>. In an **Active Directory (AD)** domain environment, the SID also includes the domain SID.

#### SID Structure:

<mark style="color:blue;">`(SID)-(revision level)-(identifier-authority)-(subauthority1)-(subauthority2)-(etc)`</mark>

<mark style="color:blue;">`S-1-5-21-674899381-4069889467-2080702030-1002`</mark>

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

When UAC is enabled, applications and tasks always run under the security context of a non-administrator account unless an administrator explicitly authorizes these applications/tasks to have administrator-level access to the system to run. It is a convenience feature that protects administrators from unintended changes but is not considered a security boundary.

With UAC enabled, a user can sign into their system using a standard account. When processes run under a standard user token, they operate with the permissions assigned to a regular user. However, certain applications need elevated privileges to function properly, and UAC allows them to receive additional access rights as needed.

When UAC is in place, an <mark style="color:orange;">**administrator user is given 2 tokens: a standard user key, to perform regular actions as regular level, and one with the admin privileges.**</mark>

The default RID 500 administrator account always operates at the high mandatory level. With <mark style="color:red;">**Admin Approval Mode (AAM)**</mark> enabled, any new admin accounts we create will operate at the medium mandatory level by default and be assigned two separate access tokens upon logging in. In the example below, the user account <mark style="color:green;">`ven17`</mark> is in the administrators group, but cmd.exe is currently running in the context of their unprivileged access token.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p><strong>UAC Strucure</strong> <a href="https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works"><strong>[SOURCE]</strong></a></p></figcaption></figure>

## <mark style="color:yellow;">NTLM</mark>

## <mark style="color:yellow;">Access Token</mark>

<mark style="color:red;">**Access tokens**</mark> in Windows <mark style="color:purple;">**define the security context of a process or thread**</mark>, including a user’s identity and privileges. When a user logs in, they are assigned an access token after successful authentication. This token is used to determine the user’s permissions whenever they interact with processes or resources.
