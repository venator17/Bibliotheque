---
icon: book-open
---

# Theory

## <mark style="color:$primary;">OS Structure</mark>

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

## <mark style="color:$primary;">SERVICES</mark>

<mark style="color:red;">**Windows Services**</mark> are <mark style="color:purple;">**long-running executable applications**</mark> that run in the background and can be automatically started when the system boots, manually started or stopped, and configured to restart upon failure. They are commonly used for core system functions, server applications, and background tasks. Service statuses can appear as <mark style="color:yellow;">**Running**</mark>, <mark style="color:yellow;">**Stopped**</mark>, or <mark style="color:yellow;">**Paused**</mark>, and they can be set to start manually, automatically, or on a delay at system boot.

#### List all running services

```powershell
Get-Service | ? {$_.Status -eq "Running"} | select -First 2 |fl
```

## <mark style="color:$primary;">PROCESSES</mark>

<mark style="color:red;">**Windows Processes**</mark> are <mark style="color:purple;">**instances of running programs or applications**</mark>. Each process contains the program's code, data, and resources required to execute tasks. Processes can run in user mode or kernel mode, and they are managed by the Windows operating system through the **Process Manager**. Also they either run automatically as part of the Windows operating system or are started by other installed applications.

## <mark style="color:$primary;">Built-in Service Accounts</mark>

#### <mark style="color:blue;">Local System Account</mark>&#x20;

<mark style="color:red;">**NT AUTHORITY\SYSTEM**</mark>, is the <mark style="color:purple;">**most powerful built-in account**</mark> in Windows. It is used by the operating system for critical tasks and services and has more privileges than local administrators.&#x20;

#### <mark style="color:blue;">Local Service Account</mark>

<mark style="color:red;">**NT AUTHORITY\LocalService**</mark>, is less privileged than the Local System Account and is used to <mark style="color:purple;">**run services with minimal rights**</mark>, having similar privileges to a standard local user.&#x20;

#### <mark style="color:blue;">Network Service Account</mark>

<mark style="color:red;">**NT AUTHORITY\NetworkService**</mark>, is used for <mark style="color:purple;">**network services that require authentication and has privileges**</mark> similar to the Local Service Account, but with the ability to access network resources.

## <mark style="color:$primary;">REGISTRY</mark>

<mark style="color:red;">**Windows Registry**</mark> is a <mark style="color:purple;">**collection of databases**</mark> of configuration settings for Windows. **The Registry** is a database of all the settings that the Microsoft Windows operating system, its applications, and hardware device drivers use to maintain their configurations.&#x20;

**The Registry** is a hierarchical database. At the top of the hierarchy is your **computer**. Under that, you’ll find the main branches, known as “<mark style="color:red;">**hives**</mark>” Within these hives are <mark style="color:red;">**Registry keys**</mark><mark style="color:red;">.</mark> Keys can contain <mark style="color:purple;">**sub-keys**</mark> and <mark style="color:purple;">**Registry values**</mark><mark style="color:purple;">.</mark>

The entire system registry is stored in several files on the operating system. You can find these under <mark style="color:green;">`C:\Windows\System32\Config\`</mark>.

The <mark style="color:red;">**user-specific registry hive (HKCU)**</mark> is stored in the user folder (<mark style="color:green;">`C:\Users\venator17\Ntuser.dat`</mark>).

<figure><img src="../../.gitbook/assets/windows_registry_structure.png" alt=""><figcaption><p>Structure of Registry</p></figcaption></figure>

### <mark style="color:blue;">Important Registry Hives</mark>

| Registry Hive                                                      | What is                                                                                                           |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| <mark style="color:green;">**`HKEY_CLASSES_ROOT (HKCR)`**</mark>   | Information about registered applications, file associations, and **OLE (Object Linking and Embedding)** objects. |
| <mark style="color:green;">**`HKEY_CURRENT_USER (HKCU)`**</mark>   | Settings specific to the current user, such as desktop settings and application settings.                         |
| <mark style="color:green;">**`HKEY_LOCAL_MACHINE (HKLM)`**</mark>  | System-wide settings, security policies, and hardware configurations that apply to all users.                     |
| <mark style="color:green;">**`HKEY_USERS (HKU)`**</mark>           | All user profiles loaded on the computer, including the current user's profile.                                   |
| <mark style="color:green;">**`HKEY_CURRENT_CONFIG (HKCC)`**</mark> | Information about the current hardware profile of the computer, such as display and printer settings.             |

### <mark style="color:blue;">Important Registry Keys</mark>

| Registry Key                                                                                                          | What is                                                                       |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| <mark style="color:green;">**`HKEY_LOCAL_MACHINE\Security`**</mark>                                                   | Security settings, such as account policies and security options.             |
| <mark style="color:green;">**`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run`**</mark>              | List of programs that run automatically at startup.                           |
| <mark style="color:green;">**`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services`**</mark>                          | Information about system services, including startup type and dependencies.   |
| <mark style="color:green;">**`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings`**</mark> | Internet Explorer settings, such as proxy settings and security zones.        |
| <mark style="color:green;">**`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Windows`**</mark>       | Windows configuration information, such as system name and installation path. |

## <mark style="color:$primary;">ICACLS</mark>

<mark style="color:red;">**ICACLS**</mark> is a <mark style="color:purple;">**command-line utility**</mark> in Windows used to **display**, **modify**, or **back up&#x20;**<mark style="color:red;">**access control lists (ACLs)**</mark> for files and directories. ACLs are used to define the permissions and access rights that users or groups have over specific files or folders.

## <mark style="color:$primary;">LLMNR & NBT-NS</mark>

<mark style="color:red;">**Link-Local Multicast Name Resolution (LLMNR)**</mark> and <mark style="color:red;">**NetBIOS Name Service (NBT-NS)**</mark> are features in Microsoft Windows that provide <mark style="color:purple;">**alternative methods for host identification**</mark> when DNS is unavailable. If a device fails to resolve a host through DNS, it will typically attempt to ask other devices on the local network for the correct host address using LLMNR. LLMNR is based on the DNS format and allows devices on the same local network to resolve names for each other. It uses UDP port 5355. If LLMNR doesn't work, NBT-NS takes over. NBT-NS identifies devices on a local network using their NetBIOS names and operates on UDP port 137. The important point is that when LLMNR or NBT-NS is used for name resolution, any device on the network can respond.

## <mark style="color:$primary;">WMI</mark>

<mark style="color:red;">**Windows Management Instrumentation (WMI)**</mark> is a <mark style="color:purple;">**subsystem of PowerShell**</mark> that provides system administrators with powerful tools for <mark style="color:purple;">**system monitoring**</mark>. The purpose of WMI is to unify the management of devices and applications across corporate networks.. WMI allows <mark style="color:yellow;">**read and write access to almost all settings**</mark> on Windows systems. Mostly uses <mark style="color:yellow;">**TCP port 135**</mark>

<mark style="color:orange;">**You can see WMI Command-Line Interface (WMIC) commands**</mark>**&#x20;for** [**\[CMD\]**](https://venator17.gitbook.io/bibliotheque/windows/commands-and-utilities#wmi) **and** [**\[PowerShell\]**](https://venator17.gitbook.io/bibliotheque/windows/powershell#wmi) here.

### <mark style="color:$primary;">**WMI Usage**</mark>

<mark style="color:red;">**WMI**</mark> can be used for a variety of purposes, including <mark style="color:purple;">**monitoring the status of local or remote systems**</mark> and <mark style="color:purple;">**configuring security settings**</mark> on remote machines or applications. It allows for <mark style="color:purple;">**managing user**</mark> and group permissions, <mark style="color:purple;">**modifying system properties**</mark>, and <mark style="color:purple;">**executing code**</mark>. Additionally, WMI supports <mark style="color:purple;">**scheduling processes**</mark> and setting up logging functionalities.

### <mark style="color:$primary;">**WMI Components**</mark>

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

## <mark style="color:$primary;">SysInternals</mark>

<mark style="color:red;">**Windows Sysinternals**</mark> is a powerful <mark style="color:purple;">**suite of utilities**</mark> created by **Mark Russinovich**, which is now owned by **Microsoft**. These tools are primarily designed for <mark style="color:yellow;">**system troubleshooting, monitoring, and diagnostics**</mark>, but they can also be extremely valuable for security researchers and ethical hackers. The tools are used to understand the internal workings of Windows, uncover security weaknesses, and perform forensic analysis. The tools can be either downloaded from the Microsoft website or by loading them directly from an internet-accessible file share by typing <mark style="color:green;">`\\live.sysinternals.com\tools`</mark> into a **Windows Explorer** window.

Examples and command you could see here: **\[LINK]**

## <mark style="color:$primary;">Named Pipes</mark>

<mark style="color:red;">**Named Pipes**</mark> in Windows are a mechanism for **inter-process communication (IPC)** that <mark style="color:purple;">**allows data exchange between processes**</mark>, either locally or across a network, using a unique name (e.g., <mark style="color:green;">`\\.\PipeName\\ExampleNamedPipeServer`</mark>). They support bidirectional communication, can transfer data securely using Windows access control, and are commonly used for client-server communication or remote management tasks. <mark style="color:orange;">**Cobalt Strike uses Named Pipes for every command (excluding BOF).**</mark>

* <mark style="color:red;">**Cobalt Strike**</mark> utilizes Named Pipes for executing commands. The process involves <mark style="color:purple;">**starting a named pipe, injecting a command into a new process, and directing the output to the pipe**</mark>, ensuring isolation from beacon crashes or antivirus detections.
* There are two types of pipes: <mark style="color:yellow;">**Named Pipes**</mark>, which are persistent and have specific names, and <mark style="color:yellow;">**Anonymous Pipes**</mark>, which are temporary and unnamed.
* The client-server model governs Named Pipes, where the server creates the pipe, and the client communicates with it. This can operate in <mark style="color:yellow;">**half-duplex**</mark> (one-way) or <mark style="color:yellow;">**duplex**</mark> (two-way) communication modes.

## <mark style="color:$primary;">Important Files Location</mark>

* <mark style="color:green;">`C:\Windows\System32\drivers\etc`</mark> _- **Local DNS file, same role as Linux****&#x20;**<mark style="color:yellow;">**/etc/hosts**</mark>_

