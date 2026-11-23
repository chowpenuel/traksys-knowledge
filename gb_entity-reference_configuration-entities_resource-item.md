# Resource Item

## Summary

### Entity Name

Resource Item

### Database Table Name

`tResourceItem`

### API Object Name

`DbResourceItem`

### Entity Description

Resource Items define individual translation strings within a Resource Group. The Resource Item key combines with the parent Resource Group key to form a translation lookup key in the format: `resx:<group_key>.<item_key>`.

## Properties

`Resource Group [ ResourceGroupID ]`

Specifies the parent Resource Group.

`Key [ Key ]`

Unique key/name for the Resource Item within the parent Resource Group. This value is the `<item_key>` portion of `resx:<group_key>.<item_key>`.

`Default Value [ DefaultValue ]`

Default (fallback) text for the resource when a localized value is not available for the requested locale.
