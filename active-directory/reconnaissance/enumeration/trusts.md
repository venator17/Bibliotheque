---
icon: arrow-right-arrow-left
---

# Trusts

## <mark style="color:yellow;">WINDOWS</mark>

#### **Checking For Trust Relationships**

```powershell
PS C:\> Get-ADTrust -Filter *
```

```powershell
C:\> netdom query /domain:militech.local trust
```

#### <mark style="color:blue;">DC Query</mark>

```cmd-session
C:\> netdom query /domain:militech.local dc
```

#### <mark style="color:blue;">Workstations and Server Query</mark>

```cmd-session
C:\> netdom query /domain:militech.local workstation
```

### <mark style="color:blue;">PowerView</mark>

#### **Trust Enumeration**

<pre class="language-powershell"><code class="lang-powershell">PS C:\> Get-DomainTrust 
<strong>
</strong><strong>PS C:\> Get-DomainTrustMapping
</strong></code></pre>

#### Check Users in Child Domain

```powershell
PS C:\> Get-DomainUser -Domain FIA.MILITECH.LOCAL | select SamAccountName
```
