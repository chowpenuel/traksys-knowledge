# Resource Group

## Summary

### Entity Name

Resource Group

### Database Table Name

`tResourceGroup`

### API Object Name

`DbResourceGroup`

### Entity Description

Resource Groups define the group key used by TrakSYS Translations (resources). Resource Groups combine with Resource Items to form a translation lookup key in the format: `resx:<group_key>.<item_key>`.

## Properties

`Key [ Key ]`

Unique key/name for the Resource Group. This value is the `<group_key>` portion of `resx:<group_key>.<item_key>`.

`Mode [ Mode ] : ETS.Core.Enums.ResourceTranslationMode`

Whether this Resource Group's Custom Translations are accessible server side, client side, or both.

* **All** = 0
* **ServerOnly** = 1
* **ClientOnly** = 2
