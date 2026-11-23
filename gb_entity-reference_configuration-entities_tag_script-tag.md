# Script Tag

## Summary

### Entity Name

Script Tag

### Database Table Name

`tTag`, `tTagScript`

### API Object Name

`DbTagScriptComposite`

### Entity Description

Script Tags allow simple and complex expressions and calculations to be created in a single Tag using .NET scripting/programming languages. There are two types of Script Tags, Simple and Advanced.

Simple Script Tag expressions are created using a VB.NET syntax. Any VB.NET language features may be used but the expression must be a single line (not physically) of code that evaluates to a single value of one of the 4 TrakSYS Tag data types (String, Integer, Float, Discrete).

Advanced Script Tag expressions are created using a C#.NET syntax. The Advanced Script Tag expression can be multiple lines of code but must end with a C# return statement which returns a single value of one of the 4 TrakSYS Tag data types (String, Integer, Float, and Discrete).

The Advanced type is only available if the Advanced Script Tag feature is licensed.

## Properties

`Script Type [ ScriptType ] : ETS.Core.Enums.TagScriptType`

Simple or Advanced (see descriptions above).

`Script [ Script ]`

Contains the expression script for this Tag.

`Auto Generate Prerequisites [ AutoGeneratePrerequisites ]`

When checked, any Tags that are referenced within the script are automatically added to this Tag's internal reference list. This value should only be unchecked when writing Advanced Script Tags that reference other Tag values by dynamically calculating their names.
