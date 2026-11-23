# Tag Group

## Summary

### Entity Name

Tag Group

### Database Table Name

`tTagGroup`

### API Object Name

`DbTagGroup`

### Entity Description

Tag Groups are solely for organizing Tags. They can be arranged in an unlimited hierarchy.

## Properties

`Parent Tag Group [ ParentTagGroupID ]`

Specifies the parent Tag Group.

`Access Path [ Access Path ]`

If present, this Access Path is used to create the full Item Name for any OPC or OPC HDA Tags directly beneath the Tag Group. The full Item Name for a Tag is made up of the OPC Server's Access Path + Parent Tag Group's Access Path + Tag's Item Name. Note that the Tag Group Access Name is NOT hierarchical. Only the Tags directly under a Tag Group get it's Access Path setting applied.
