---
icon: tombstone-blank
---

# Tombstone

## <mark style="color:yellow;">ABOUT</mark>

Tombstone in Active Directory is a logically deleted object that's kept for a limited time (default: 180 days) to allow deletion to replicate across domain controllers. It retains critical attributes like <mark style="color:green;">`objectSID`</mark>, <mark style="color:green;">`objectGUID`</mark>, and <mark style="color:green;">`lastKnownParent`</mark>, enabling potential object recovery. After the tombstone lifetime, the object is permanently removed by garbage collection. Tombstones help prevent lingering objects and replication conflicts.

### <mark style="color:blue;">Zombie Objects</mark>

For better explanation you need to imagine a scenario. You have DC1 and DC2. You have same object (user) Bob on both of DC's. Replication technology is used to sync objects between these two. But DC1 is going offline. During that time, Bob is deleted, tombstone is made and replicated. Then after 180 days all tombstones are deleted. Then DC1 is getting back online, and there is not tombstone to notify DC1 that Bob was deleted. Because of that DC1 thinks that bob is valid user, and replicates it across all Domain.

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
