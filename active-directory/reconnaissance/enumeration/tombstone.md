---
icon: tombstone-blank
---

# Tombstone

## <mark style="color:yellow;">ABOUT</mark>

Tombstone in Active Directory is a logically deleted object that's kept for a limited time (default: 180 days) to allow deletion to replicate across domain controllers. It retains critical attributes like <mark style="color:green;">`objectSID`</mark>, <mark style="color:green;">`objectGUID`</mark>, and <mark style="color:green;">`lastKnownParent`</mark>, enabling potential object recovery. After the tombstone lifetime, the object is permanently removed by garbage collection. Tombstones help prevent lingering objects and replication conflicts.

## <mark style="color:yellow;">LOCATING</mark>

### Computers

```powershell
Get-ADObject -Filter 'isDeleted -eq $true -and objectClass -eq "computer"' -IncludeDeletedObjects
```

### Users

```powershell
Get-ADObject -Filter 'isDeleted -eq $true -and objectClass -eq "user"' -IncludeDeletedObjects
```

### Groups

```powershell
Get-ADObject -Filter 'isDeleted -eq $true -and objectClass -eq "group"' -IncludeDeletedObjects
```

## <mark style="color:yellow;">TECHNO-NECROMANCY</mark>

> Restoring dead objects

```powershell
Restore-ADObject -Identity '<ObjectGUID>'
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.itprotoday.com/active-directory/ad-tombstone-objects" %}
