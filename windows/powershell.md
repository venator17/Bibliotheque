---
icon: square-terminal
---

# PowerShell

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**PowerShell**</mark> is a powerful task automation and configuration management <mark style="color:purple;">**framework**</mark> developed by Microsoft, built on the .NET framework. It includes a command-line shell and a <mark style="color:purple;">**scripting language**</mark> designed to automate tasks across Windows systems, such as managing processes, services, files, and configurations. **PowerShell** is more powerful and flexible than the traditional **Command Prompt (cmd)** and integrates deeply with system administration tools.

<mark style="color:orange;">**ALSO WE COULD USE CMD COMMANDS WITH**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`CMD /C {COMMAND}`</mark>

## <mark style="color:yellow;">ALIASES</mark>

Many cmdlets in PowerShell also have <mark style="color:red;">**aliases**</mark>. For example, the aliases for the cmdlet <mark style="color:green;">`Set-Location`</mark>, to change directories, is either <mark style="color:green;">`cd`</mark> or <mark style="color:green;">`sl`</mark>. We can view all available aliases by typing <mark style="color:green;">**`Get-Alias`**</mark>.

```powershell
PS C:\> get-alias

CommandType     Name                               Version    Source
-----------     ----                               -------    ------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           asnp -> Add-PSSnapin
Alias           cat -> Get-Content
Alias           cd -> Set-Location
```

We can also set up our own aliases with <mark style="color:green;">`New-Alias`</mark> and get the alias for any cmdlet with <mark style="color:green;">`Get-Alias -Name`</mark>.

```powershell
PS C:\> New-Alias -Name "Show-Files" Get-ChildItem
PS C:\> Get-Alias -Name "Show-Files"

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Show-Files
```

## <mark style="color:yellow;">RUNNING SCRIPTS</mark>

<mark style="color:red;">**PowerShell ISE (Integrated Scripting Environment)**</mark> allows users to <mark style="color:purple;">**write PowerShell scripts on the fly**</mark>. It also has an autocomplete/lookup function for PowerShell commands. The PowerShell ISE allows us to write and run scripts in the same console, which allows for quick debugging.

#### Examples:

```powershell
PS C:\> .\PowerView.ps1; Get-LocalGroup | fl
```

Import scripts so that all functions could be used in our PowerShell session

```powershell
PS C:\> Import-Module .\PowerView.ps1
```

## <mark style="color:yellow;">EXECUTION POLICY</mark>

<mark style="color:red;">**Execution Policy**</mark>, is security feature to <mark style="color:purple;">**control script execution**</mark> and prevent the execution of malicious scripts.&#x20;

<mark style="color:orange;">**Execution policy is not a security boundary**</mark> and can be <mark style="color:purple;">**bypassed**</mark> by&#x20;

* Typing the script directly into the console.
* Using encoded commands or adjusting policy temporarily.

#### Changing the execution policy for the current process (session).

```powershell
PS C:\> Set-ExecutionPolicy Bypass -Scope Process
```

#### View execution policy

<pre class="language-powershell"><code class="lang-powershell"><strong>PS C:\> Get-ExecutionPolicy -List
</strong></code></pre>

| Policy                                            | Description                                                                                                                         |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| <mark style="color:blue;">**AllSigned**</mark>    | Scripts need a trusted publisher's signature. Prompts for untrusted publishers.                                                     |
| <mark style="color:blue;">**Bypass**</mark>       | No restrictions; no warnings or prompts.                                                                                            |
| <mark style="color:blue;">**Default**</mark>      | Default: <mark style="color:green;">`Restricted`</mark> for desktops, <mark style="color:green;">`RemoteSigned`</mark> for servers. |
| <mark style="color:blue;">**RemoteSigned**</mark> | Local scripts can run; downloaded scripts require a digital signature.                                                              |
| <mark style="color:blue;">**Restricted**</mark>   | Blocks script execution; allows individual commands.                                                                                |
| <mark style="color:blue;">**Undefined**</mark>    | No policy set; defaults to <mark style="color:green;">`Restricted`</mark>.                                                          |
| <mark style="color:blue;">**Unrestricted**</mark> | Allows unsigned scripts; warns for non-local intranet scripts.                                                                      |

## <mark style="color:yellow;">CMDLETS</mark>

<mark style="color:red;">**Cmdlets**</mark> are <mark style="color:purple;">**specialized commands**</mark> in **PowerShell**. They follow a consistent verb-noun naming (<mark style="color:green;">**`Get-Process`**</mark>) to indicate their action and the object they operate on.

#### Get more info about file

```powershell
PS C:\> Get-ChildItem -Path 'C:\Share\file.txt' | Select Fullname,LastWriteTime,Attributes,@{Name="Owner";Expression={ (Get-Acl $_.FullName).Owner }}
```

#### List all running Services

```powershell
PS C:\> Get-Service | ? {$_.Status -eq "Running"} | select -First 2 | fl
```

#### Examine Service permissions

```powershell
PS C:\> Get-ACL -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List
```

#### List all loaded Modules

```powershell
PS C:\> Get-Module | select Name,ExportedCommands | fl
```

#### Check Defender

```powershell
PS C:\> Get-MpComputerStatus | findstr "True"
```

#### **Listing Named Pipes**

```powershell
PS C:\> gci \\.\pipe\
```

## <mark style="color:yellow;">WMI</mark>

#### Getting Windows Version

```powershell
PS C:\> Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber
```

#### List system information

```powershell
PS C:\> Get-WmiObject -Class Win32_OperatingSystem | select SystemDirectory,BuildNumber,SerialNumber,Version | ft
```

#### Get SID of users

```powershell
PS C:\> get-localuser | Select name,sid
```

#### Get all service paths

```powershell
PS C:\> wmic service get name, pathname
```
