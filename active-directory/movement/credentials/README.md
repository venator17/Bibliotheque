---
icon: key
---

# Credentials

## <mark style="color:yellow;">Password in Description Field</mark>

Sensitive information such as account passwords are sometimes found in the user account **Description** or **Notes** fields and can be quickly enumerated using PowerView.

```powershell
PS C:\> Get-DomainUser * | Select-Object samaccountname,description |Where-Object {$_.Description -ne $null}
```
