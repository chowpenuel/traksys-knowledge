# Script Class Tag

## Summary

### Entity Name

Script Class Tag

### Database Table Name

`tTag`, `tTagScriptClass`

### API Object Name

`DDbTagScriptClassComposite`

### Entity Description

Script Class Tags, similar to Script Tags, can be used to execute C# code to help process complex logic.

Unlike a Script Tag which create a separate C# class and instance of the Tag, a Script Class Tag references a single Tag Script Class within the TrakSYS configuration. Since Script Class Tags reference a singular Script Class, any changes to the Script Class will automatically apply to all Script Class Tags referencing that class.

## Properties

`Script Class Name [ScriptClassName]`

Specifies Tag Script Class Name that will be referenced.

`Source Tag IDs [ Source01TagID - Source10TagID ]`

Specifies Tag ID which can be referenced within a Tag Script Class.

`Parameters [ Param01 - Param05 ]`

Specifies static value that can be referenced within a Tag Script Class.
