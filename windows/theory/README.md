---
icon: book-open
---

# Theory

## <mark style="color:yellow;">OS Structure</mark>

In Windows, the root directory is <mark style="color:green;">**\<drive\_letter>:\\**</mark> (usually **C:**), where the OS is installed. Other drives, like Data **(E:),** are assigned different letters. The boot partition’s directory structure includes key system folders:

| Directory                                                       | Function                                                                                                         |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| <mark style="color:blue;">**Perflogs**</mark>                   | Holds performance logs (empty by default).                                                                       |
| <mark style="color:blue;">**Program Files**</mark>              | Contains 64-bit programs on 64-bit systems, 32-bit programs on 32-bit systems.                                   |
| <mark style="color:blue;">**Program Files (x86)**</mark>        | Stores 32-bit programs on 64-bit systems.                                                                        |
| <mark style="color:blue;">**ProgramData**</mark>                | Hidden folder for essential program data shared by all users.                                                    |
| <mark style="color:blue;">**Users**</mark>                      | Stores user profiles and includes Public and Default folders.                                                    |
| <mark style="color:blue;">**Default**</mark>                    | Template for creating new user profiles.                                                                         |
| <mark style="color:blue;">**Public**</mark>                     | Shared folder accessible to all users and over the network.                                                      |
| <mark style="color:blue;">**AppData**</mark>                    | Hidden per-user folder with Roaming (synced), Local (machine-specific), and LocalLow (low integrity) subfolders. |
| <mark style="color:blue;">**Windows**</mark>                    | Contains core files for the Windows operating system.                                                            |
| <mark style="color:blue;">**System, System32, SysWOW64**</mark> | Holds essential DLLs for Windows and its API.                                                                    |
| <mark style="color:blue;">**WinSxS**</mark>                     | Stores copies of all Windows components and updates.                                                             |

## <mark style="color:yellow;">NTFS Permissions</mark>

| Permission Type                                           | Description                                                                                             |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| <mark style="color:blue;">**Full Control**</mark>         | Allows reading, writing, changing, and deleting files/folders.                                          |
| <mark style="color:blue;">**Modify**</mark>               | Allows reading, writing, and deleting files/folders.                                                    |
| <mark style="color:blue;">**List Folder Contents**</mark> | Allows viewing and listing folders/subfolders and executing files. Folders inherit this permission.     |
| <mark style="color:blue;">**Read and Execute**</mark>     | Allows viewing, listing files/subfolders, and executing files. Inherited by both files and folders.     |
| <mark style="color:blue;">**Write**</mark>                | Allows adding files to folders and writing to a file.                                                   |
| <mark style="color:blue;">**Read**</mark>                 | Allows viewing and listing folders/subfolders and reading file contents.                                |
| <mark style="color:blue;">**Traverse Folder**</mark>      | Allows moving through folders to access files, even without permission to list or view folder contents. |

## <mark style="color:yellow;">SERVICES</mark>

<mark style="color:red;">**Windows Services**</mark> are <mark style="color:purple;">**long-running executable applications**</mark> that run in the background and can be automatically started when the system boots, manually started or stopped, and configured to restart upon failure. They are commonly used for core system functions, server applications, and background tasks. Service statuses can appear as <mark style="color:yellow;">**Running**</mark>, <mark style="color:yellow;">**Stopped**</mark>, or <mark style="color:yellow;">**Paused**</mark>, and they can be set to start manually, automatically, or on a delay at system boot.

#### List all running services

```powershell
Get-Service | ? {$_.Status -eq "Running"} | select -First 2 |fl
```

## <mark style="color:yellow;">PROCESSES</mark>

<mark style="color:red;">**Windows Processes**</mark> are <mark style="color:purple;">**instances of running programs or applications**</mark>. Each process contains the program's code, data, and resources required to execute tasks. Processes can run in user mode or kernel mode, and they are managed by the Windows operating system through the **Process Manager**. Also they either run automatically as part of the Windows operating system or are started by other installed applications.

## <mark style="color:yellow;">Built-in Service Accounts</mark>

#### <mark style="color:blue;">Local System Account</mark>&#x20;

<mark style="color:red;">**NT AUTHORITY\SYSTEM**</mark>, is the <mark style="color:purple;">**most powerful built-in account**</mark> in Windows. It is used by the operating system for critical tasks and services and has more privileges than local administrators.&#x20;

#### <mark style="color:blue;">Local Service Account</mark>

<mark style="color:red;">**NT AUTHORITY\LocalService**</mark>, is less privileged than the Local System Account and is used to <mark style="color:purple;">**run services with minimal rights**</mark>, having similar privileges to a standard local user.&#x20;

#### <mark style="color:blue;">Network Service Account</mark>

<mark style="color:red;">**NT AUTHORITY\NetworkService**</mark>, is used for <mark style="color:purple;">**network services that require authentication and has privileges**</mark> similar to the Local Service Account, but with the ability to access network resources.

## <mark style="color:yellow;">REGISTRY</mark>

<mark style="color:red;">**Windows Registry**</mark> is a <mark style="color:purple;">**collection of databases**</mark> of configuration settings for Windows. **The Registry** is a database of all the settings that the Microsoft Windows operating system, its applications, and hardware device drivers use to maintain their configurations.&#x20;

**The Registry** is a hierarchical database. At the top of the hierarchy is your **computer**. Under that, you’ll find the main branches, known as “<mark style="color:red;">**hives**</mark>” Within these hives are <mark style="color:red;">**Registry keys**</mark><mark style="color:red;">.</mark> Keys can contain <mark style="color:purple;">**sub-keys**</mark> and <mark style="color:purple;">**Registry values**</mark><mark style="color:purple;">.</mark>

The entire system registry is stored in several files on the operating system. You can find these under <mark style="color:green;">`C:\Windows\System32\Config\`</mark>.

The <mark style="color:red;">**user-specific registry hive (HKCU)**</mark> is stored in the user folder (<mark style="color:green;">`C:\Users\venator17\Ntuser.dat`</mark>).

<figure><img src="../../.gitbook/assets/windows_registry_structure.png" alt=""><figcaption><p>Structure of Registry</p></figcaption></figure>

### <mark style="color:blue;">Important Registry Hives</mark>

| Registry Hive                                                     | What is                                                                                                           |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| <mark style="color:blue;">**HKEY\_CLASSES\_ROOT (HKCR)**</mark>   | Information about registered applications, file associations, and **OLE( Object Linking and Embedding)** objects. |
| <mark style="color:blue;">**HKEY\_CURRENT\_USER (HKCU)**</mark>   | Settings specific to the current user, such as desktop settings and application settings.                         |
| <mark style="color:blue;">**HKEY\_LOCAL\_MACHINE (HKLM)**</mark>  | System-wide settings, security policies, and hardware configurations that apply to all users.                     |
| <mark style="color:blue;">**HKEY\_USERS (HKU)**</mark>            | All user profiles loaded on the computer, including the current user's profile.                                   |
| <mark style="color:blue;">**HKEY\_CURRENT\_CONFIG (HKCC)**</mark> | Information about the current hardware profile of the computer, such as display and printer settings.             |

### <mark style="color:blue;">Important Registry Keys</mark>

| Registry Key                                                                                                         | What is                                                                       |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| <mark style="color:blue;">**HKEY\_LOCAL\_MACHINE\Security**</mark>                                                   | Security settings, such as account policies and security options.             |
| <mark style="color:blue;">**HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run**</mark>              | List of programs that run automatically at startup.                           |
| <mark style="color:blue;">**HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Services**</mark>                          | Information about system services, including startup type and dependencies.   |
| <mark style="color:blue;">**HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings**</mark> | Internet Explorer settings, such as proxy settings and security zones.        |
| <mark style="color:blue;">**HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Windows**</mark>       | Windows configuration information, such as system name and installation path. |

## <mark style="color:yellow;">ICACLS</mark>

<mark style="color:red;">**ICACLS**</mark> is a <mark style="color:purple;">**command-line utility**</mark> in Windows used to **display**, **modify**, or **back up&#x20;**<mark style="color:red;">**access control lists (ACLs)**</mark> for files and directories. ACLs are used to define the permissions and access rights that users or groups have over specific files or folders.b

#### **Explanation of Inheritance**

Inheritance in NTFS allows permissions to propagate from a parent folder to its subfolders and files. This ensures consistent permissions throughout a directory structure. Modifiers like <mark style="color:blue;">**`(CI)`**</mark>, <mark style="color:blue;">**`(OI)`**</mark>, and <mark style="color:blue;">**`(IO)`**</mark> define how permissions are inherited by child objects.

#### **Inheritance Modifiers**

| Modifier                                  | Meaning                              | Explanation                                                                 |
| ----------------------------------------- | ------------------------------------ | --------------------------------------------------------------------------- |
| <mark style="color:blue;">**`CI`**</mark> | **Container Inherit**                | Applies permissions to subfolders (but not files) within the parent folder. |
| <mark style="color:blue;">**`OI`**</mark> | **Object Inherit**                   | Applies permissions to files (but not subfolders) within the parent folder. |
| <mark style="color:blue;">**`IO`**</mark> | **Inherit Only**                     | Ensures permissions are inherited but not applied directly to the parent.   |
| <mark style="color:blue;">**`NP`**</mark> | **Do Not Propagate Inherit**         | Prevents permissions from propagating further to child objects.             |
| <mark style="color:blue;">**`I`**</mark>  | **Permission Inherited from Parent** | Indicates that the permission was inherited from a parent container.        |

#### **Basic Access Permissions**

<table><thead><tr><th>Symbol</th><th width="286">Permission</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong><code>F</code></strong></mark></td><td><strong>Full Access</strong></td><td>Grants all permissions, including modifying and deleting.</td></tr><tr><td><mark style="color:blue;"><strong><code>D</code></strong></mark></td><td><strong>Delete Access</strong></td><td>Allows deletion of the file or folder.</td></tr><tr><td><mark style="color:blue;"><strong><code>N</code></strong></mark></td><td><strong>No Access</strong></td><td>Denies all access to the file or folder.</td></tr><tr><td><mark style="color:blue;"><strong><code>M</code></strong></mark></td><td><strong>Modify Access</strong></td><td>Allows reading, writing, and deleting content.</td></tr><tr><td><mark style="color:blue;"><strong><code>RX</code></strong></mark></td><td><strong>Read &#x26; Execute</strong></td><td>Allows reading and executing files.</td></tr><tr><td><mark style="color:blue;"><strong><code>R</code></strong></mark></td><td><strong>Read-Only Access</strong></td><td>Permits viewing and listing of contents.</td></tr><tr><td><mark style="color:blue;"><strong><code>W</code></strong></mark></td><td><strong>Write-Only Access</strong></td><td>Allows adding new files and data but not reading.</td></tr></tbody></table>

## <mark style="color:yellow;">DPAPI</mark>

<mark style="color:red;">**Data Protection Application Programming Interface**</mark> is set of API which Windows uses for the symmetric encryption of asymmetric private keys and used by various third-party applications like:

* **Internet Explorer**
* **Google Chrome**
* **Outlook**
* **Remote Desktop Connection**
* **Credential Manager**

## <mark style="color:yellow;">WMI</mark>

<mark style="color:red;">**Windows Management Instrumentation (WMI)**</mark> is a <mark style="color:purple;">**subsystem of PowerShell**</mark> that provides system administrators with powerful tools for <mark style="color:purple;">**system monitoring**</mark>. The purpose of WMI is to unify the management of devices and applications across corporate networks.. WMI allows <mark style="color:yellow;">**read and write access to almost all settings**</mark> on Windows systems. Mostly uses <mark style="color:yellow;">**TCP port 135**</mark>

<mark style="color:orange;">**You can see WMI Command-Line Interface (WMIC) commands**</mark>**&#x20;for&#x20;**<mark style="color:blue;">**\[CMD]**</mark>**&#x20;and&#x20;**<mark style="color:blue;">**\[PowerShell]**</mark> here.

### <mark style="color:blue;">**WMI Usage**</mark>

<mark style="color:red;">**WMI**</mark> can be used for a variety of purposes, including <mark style="color:purple;">**monitoring the status of local or remote systems**</mark> and <mark style="color:purple;">**configuring security settings**</mark> on remote machines or applications. It allows for <mark style="color:purple;">**managing user**</mark> and group permissions, <mark style="color:purple;">**modifying system properties**</mark>, and <mark style="color:purple;">**executing code**</mark>. Additionally, WMI supports <mark style="color:purple;">**scheduling processes**</mark> and setting up logging functionalities.

### <mark style="color:blue;">**WMI Components**</mark>

| **Component**                                           | **Description**                                                                           |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| <mark style="color:blue;">**WMI Service**</mark>        | Runs at boot and acts as an intermediary between providers, repository, and applications. |
| <mark style="color:blue;">**Managed Objects**</mark>    | Logical or physical components managed by WMI.                                            |
| <mark style="color:blue;">**WMI Providers**</mark>      | Monitor events and data for specific objects.                                             |
| <mark style="color:blue;">**Classes**</mark>            | Pass data to the WMI service via providers.                                               |
| <mark style="color:blue;">**Methods**</mark>            | Enable actions such as starting or stopping processes.                                    |
| <mark style="color:blue;">**WMI Repository**</mark>     | Stores static WMI data.                                                                   |
| <mark style="color:blue;">**CIM Object Manager**</mark> | Handles data requests and responses.                                                      |
| <mark style="color:blue;">**WMI API**</mark>            | Allows applications to access the WMI infrastructure.                                     |
| <mark style="color:blue;">**WMI Consumer**</mark>       | Queries objects via the CIM Object Manager.                                               |

#### Tips2Hack

1. <mark style="color:green;">**WMIexec.py**</mark>

```bash
/usr/share/doc/python3-impacket/examples/wmiexec.py venator17:"4m0gus"@13.13.13.13 "hostname"
```

2. Get all service paths

```powershell
wmic service get name, pathname
```

## <mark style="color:yellow;">SysInternals</mark>

<mark style="color:red;">**Windows Sysinternals**</mark> is a powerful <mark style="color:purple;">**suite of utilities**</mark> created by **Mark Russinovich**, which is now owned by **Microsoft**. These tools are primarily designed for <mark style="color:yellow;">**system troubleshooting, monitoring, and diagnostics**</mark>, but they can also be extremely valuable for security researchers and ethical hackers. The tools are used to understand the internal workings of Windows, uncover security weaknesses, and perform forensic analysis. The tools can be either downloaded from the Microsoft website or by loading them directly from an internet-accessible file share by typing <mark style="color:green;">`\\live.sysinternals.com\tools`</mark> into a **Windows Explorer** window.

Examples and command you could see here: **\[LINK]**

## Important Files Location

* <mark style="color:green;">`C:\Windows\System32\drivers\etc`</mark> _- **Local DNS file, same role as Linux****&#x20;**<mark style="color:yellow;">**/etc/hosts**</mark>_

