---
icon: books
---

# Terminology

## <mark style="color:yellow;">Object</mark>

* Object can be defined as ANY resource present within an Active Directory environment such as OUs, printers, users, domain controllers.

## <mark style="color:yellow;">Global Unique Identifier (GUID)</mark>

* Unique 128-bit value assigned to objects.
* Used internally by AD for identification.

## <mark style="color:yellow;">Security Principals</mark>

* Authenticated entities (users, computers, services, etc.).
* Manage access to domain resources.

## <mark style="color:yellow;">Distinguished Name (DN)</mark>

* Full path to an object in AD (e.g., <mark style="color:blue;">`cn=sreed, ou=IT, dc=example, dc=com`</mark>).

## <mark style="color:yellow;">Relative Distinguished Name (RDN)</mark>

* Unique identifier within its parent container.

## <mark style="color:yellow;">userPrincipalName (UPN)</mark>

* Alternative way to identify users (e.g., <mark style="color:blue;">`sreed@example.com`</mark>).

## <mark style="color:yellow;">FSMO Roles</mark>

* Five roles ensuring AD replication and operation:
  1. <mark style="color:blue;">**Schema Master**</mark> (one per forest)
  2. <mark style="color:blue;">**Domain Naming Master**</mark> (one per forest)
  3. <mark style="color:blue;">**RID Master**</mark> (one per domain)
  4. <mark style="color:blue;">**PDC Emulator**</mark> (one per domain)
  5. <mark style="color:blue;">**Infrastructure Master**</mark> (one per domain)

## <mark style="color:yellow;">Global Catalog (GC)</mark>

* Stores full copies of objects in the current domain and partial copies from other domains.
* Helps in authentication and searching for AD objects across domains.
* Crucial for login processes and Exchange Server lookups.

## <mark style="color:yellow;">Replication</mark>

* Synchronizes changes across Domain Controllers.
* Managed by the Knowledge Consistency Checker (KCC).

## <mark style="color:yellow;">Service Principal Name (SPN)</mark>

* <mark style="color:red;">**Service Principal Name (SPN)**</mark> is a <mark style="color:purple;">**unique identifier**</mark> of a service instance. Kerberos authentication uses SPNs to associate a service instance with a service sign-in account. Doing so allows a client application to request service authentication for an account even if the client doesn't have the account name, because every service has a corresponding service account.

## <mark style="color:yellow;">Group Policy Object (GPO)</mark>

* Collection of policy settings applied to users and computers.
* Used for security configurations, software deployments, and administrative settings.
* Can be applied at different levels (site, domain, OU).

## <mark style="color:yellow;">Fully Qualified Domain Name (FQDN)</mark>

* Complete name for a host (e.g., <mark style="color:green;">`dc01.example.com`</mark>).

## <mark style="color:yellow;">SYSVOL</mark>

* Stores Group Policy settings and logon scripts.
* Replicated across all DCs.

## <mark style="color:yellow;">ADSI Edit</mark>

* Advanced GUI tool for managing AD objects and attributes.

## <mark style="color:yellow;">sIDHistory</mark>

* Stores previous SIDs during migrations.
* Can be abused if not secured.
