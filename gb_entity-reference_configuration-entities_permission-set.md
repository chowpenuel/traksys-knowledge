# Permission Set

## Summary

### Entity Name

Permission Set

### Database Table Name

`tPermissionSet`

### API Object Name

`DbPermissionSet`

### Entity Description

Permission Sets define a named permission grouping used by TrakSYS security. The Set Type determines whether permissions in the set are defined as a flat Set/Action list or as a Set/Action/Item grid.

## Properties

`Key [ Key ]`

Unique identifier for the Permission Set, and the identifier used by the API when requesting permission data for this set.

`Set Type [ SetType ] : ETS.Core.Enums.PermissionSetType`

This is an enumeration representing how permissions are structured for the Permission Set.

* **Flat** = 0
* **Grid** = 1

**Flat** - Used for permissions that have **Set** and **Action** only (no Item).

**Grid** - Used for permissions that have **Set**, **Action**, and **Item**.
