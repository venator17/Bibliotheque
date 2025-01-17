---
icon: screwdriver-wrench
---

# Commands and Utilities

## <mark style="color:yellow;">CMD COMMAND</mark>

1. After launching <mark style="color:green;">**`cmd.exe`**</mark> we can type <mark style="color:green;">`help`</mark> to see a listing of available commands.
2. For more information about a specific command, we can type <mark style="color:green;">`help <command name>`</mark>.
3. Certain commands have their own help menus, which can be accessed by typing <mark style="color:green;">`<command> /?`</mark>.&#x20;

### <mark style="color:yellow;">DIR</mark>

Windows command that <mark style="color:purple;">**lists the contents**</mark> of a **directory**, including **files** and **subfolders.**

| Command                                       | Explanation                                                       |
| --------------------------------------------- | ----------------------------------------------------------------- |
| <mark style="color:green;">`dir`</mark>       | Lists files and subdirectories in the current directory.          |
| <mark style="color:green;">`dir /s`</mark>    | Displays files in the specified directory and all subdirectories. |
| <mark style="color:green;">`dir /a`</mark>    | Shows hidden and system files.                                    |
| <mark style="color:green;">`dir /p`</mark>    | Lists contents one page at a time.                                |
| <mark style="color:green;">`dir /w`</mark>    | Displays results in a wide format.                                |
| <mark style="color:green;">`dir *.txt`</mark> | Displays all txt files                                            |
| <mark style="color:green;">`dir /t:c`</mark>  | Lists files sorted by creation time                               |
| <mark style="color:green;">`dir /o:n`</mark>  | Lists files and folders sorted alphabetically                     |

### <mark style="color:yellow;">TREE</mark>

Windows command that <mark style="color:purple;">**displays the directory structure**</mark> in a **tree-like** format.

| Command                                      | Explanation                                                      |
| -------------------------------------------- | ---------------------------------------------------------------- |
| <mark style="color:green;">`tree`</mark>     | Displays the directory structure of the current folder.          |
| <mark style="color:green;">`tree /f`</mark>  | Shows the directory structure including files.                   |
| <mark style="color:green;">`tree /a`</mark>  | Uses ASCII characters for lines instead of extended characters.  |
| <mark style="color:green;">`tree /p`</mark>  | Displays the tree one page at a time (useful for large outputs). |
| <mark style="color:green;">`tree D:\`</mark> | Displays the directory structure of a specific drive.            |

### <mark style="color:yellow;">TYPE</mark>

Windows command that <mark style="color:purple;">**displays the contents of a text file.**</mark>

| Command                                                        | Explanation                                               |
| -------------------------------------------------------------- | --------------------------------------------------------- |
| <mark style="color:green;">`type file.txt`</mark>              | Displays the entire content of **`file.txt`**.            |
| <mark style="color:green;">`type file1.txt file2.txt`</mark>   | Concatenates and displays the contents of multiple files. |
| <mark style="color:green;">`type file.txt > output.txt`</mark> | Redirects the output to a new file **`output.txt`**.      |

### <mark style="color:yellow;">ICACLS</mark>

Windows command that <mark style="color:purple;">**manages permissions**</mark> for files and directories.

| Command                                                        | Explanation                                                                            |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| <mark style="color:green;">`icacls <filename>`</mark>          | Displays the current access control list (ACL) for the specified file.                 |
| <mark style="color:green;">`icacls <directory>`</mark>         | Displays the ACLs for all files and subdirectories in the specified directory.         |
| <mark style="color:green;">`icacls <filename> /grant`</mark>   | Grants specified permissions to a user or group for the specified file.                |
| <mark style="color:green;">`icacls <filename> /deny`</mark>    | Denies specified permissions to a user or group for the specified file.                |
| <mark style="color:green;">`icacls <filename> /remove`</mark>  | Removes all granted permissions for a specified user or group from the specified file. |
| <mark style="color:green;">`icacls <filename> /save`</mark>    | Saves the ACLs of files and directories to a specified file for later restoration.     |
| <mark style="color:green;">`icacls <filename> /restore`</mark> | Restores the saved ACLs from a file to the specified files or directories.             |

### <mark style="color:yellow;">NET</mark>

Windows command used for <mark style="color:purple;">**managing network resources**</mark>, services, and user accounts.

| Command                                                 | Explanation                                                                  |
| ------------------------------------------------------- | ---------------------------------------------------------------------------- |
| <mark style="color:green;">`net use`</mark>             | Connects to a shared resource (e.g., network drive or printer).              |
| <mark style="color:green;">`net user`</mark>            | Manages local user accounts (e.g., create, delete, or modify user accounts). |
| <mark style="color:green;">`net share`</mark>           | Displays or manages shared resources on the local computer.                  |
| <mark style="color:green;">`net view`</mark>            | Displays a list of shared resources or computers on the network.             |
| <mark style="color:green;">`net stop <service>`</mark>  | Stops a specified Windows service.                                           |
| <mark style="color:green;">`net start <service>`</mark> | Starts a specified Windows service.                                          |
| <mark style="color:green;">`net localgroup`</mark>      | Manages local groups by adding or removing users.                            |
| <mark style="color:green;">`net accounts`</mark>        | Configures password and logon requirements for local user accounts.          |

### <mark style="color:yellow;">**SC**</mark>

Windows command that <mark style="color:purple;">**manages services**</mark>, allowing users to **query, start, stop, configure, and delete services** locally or remotely.

| Command                                                                              | Explanation                                                                |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| <mark style="color:green;">`sc qc <ServiceName>`</mark>                              | Queries the configuration of a specific service.                           |
| <mark style="color:green;">`sc \\<hostname_or_ip> query <ServiceName>`</mark>        | Queries the status of a service on a remote machine.                       |
| <mark style="color:green;">`sc start <ServiceName>`</mark>                           | Starts a specified service.                                                |
| <mark style="color:green;">`sc stop <ServiceName>`</mark>                            | Stops a specified service.                                                 |
| <mark style="color:green;">`sc config <ServiceName> binPath=<NewPath>`</mark>        | Changes the executable path of a service, useful for privilege escalation. |
| <mark style="color:green;">`sc sdshow <ServiceName>`</mark>                          | Displays the security descriptor (permissions) of a service.               |
| <mark style="color:green;">`sc delete <ServiceName>`</mark>                          | Deletes a specified service.                                               |
| <mark style="color:green;">`sc \\<hostname_or_ip> stop <ServiceName>`</mark>         | Stops a service on a remote machine.                                       |
| <mark style="color:green;">`sc failure <ServiceName> reset=<Time>`</mark>            | Configures a service to reset its failure count after a specific time.     |
| <mark style="color:green;">`sc failure <ServiceName> actions=restart/<Delay>`</mark> | Configures a service to restart after failure, useful for persistence.     |
| <mark style="color:green;">`sc \\<hostname_or_ip> qc <ServiceName>`</mark>           | Queries the configuration of a service on a remote machine.                |
| <mark style="color:green;">`sc interrogate <ServiceName>`</mark>                     | Forces the service to report its current status immediately.               |
| <mark style="color:green;">`sc triggerinfo <ServiceName>`</mark>                     | Displays the triggers that start or stop a service automatically.          |
| <mark style="color:green;">`sc pause <ServiceName>`</mark>                           | Pauses a running service.                                                  |
| <mark style="color:green;">`sc continue <ServiceName>`</mark>                        | Resumes a paused service.                                                  |

## <mark style="color:yellow;">**SYSINTERNALS**</mark>

<mark style="color:red;">**Windows Sysinternals**</mark> is a powerful <mark style="color:purple;">**suite of utilities**</mark> created by **Mark Russinovich**, which is now owned by **Microsoft**. These tools are primarily designed for <mark style="color:yellow;">**system troubleshooting, monitoring, and diagnostics**</mark>, but they can also be extremely valuable for security researchers and ethical hackers.

### PsExec

<mark style="color:red;">**PsExec**</mark> is a command-line <mark style="color:purple;">**tool**</mark> from the <mark style="color:yellow;">**Windows Sysinternals**</mark> suite that allows you to execute processes on remote systems without needing to manually install client software. It works over **SMB (Server Message Block)**, enabling remote command execution on Windows machines, making it a powerful tool for both system administration and ethical hacking.

**Usage** (same things to <mark style="color:green;">**`impacket-smbexec`**</mark> and <mark style="color:green;">**`impacket-atexec`**</mark>):

```bash
impacket-psexec administrator:'amoguskek'@13.13.13.13
```

## <mark style="color:yellow;">WMI</mark>

A lot of tasks with WMI can all be performed using a combination of PowerShell and the WMI <mark style="color:red;">**Command-Line Interface (WMIC)**</mark>. We can view a listing of WMIC commands and aliases by typing <mark style="color:green;">`WMIC /?`</mark>

#### List system information:&#x20;

```powershell
C:\> wmic os list brief
```
