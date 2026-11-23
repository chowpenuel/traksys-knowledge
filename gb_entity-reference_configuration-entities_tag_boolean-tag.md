# Boolean Tag

## Summary

### Entity Name

Boolean Tag

### Database Table Name

`tTag`, `tTagBoolean`

### API Object Name

`DbTagBooleanComposite`

### Entity Description

Boolean Tags allow you to combine the values of two or more Tags using logical AND, OR, XOR, NAND, NOR, and XNOR operations. You can also specify what values to return if the Boolean operation evaluates to True or False, using either constants or Tags.

## Properties

`Operation [ Operation ] : ETS.Core.Enums.TagBooleanOperation`

Boolean operation to perform on the specified list of Tags. Select **AND**, **OR**, **XOR**, **NAND**, **NOR**, or **XNOR**.
