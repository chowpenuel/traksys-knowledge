# Compare Tag

## Summary

### Entity Name

Compare Tag

### Database Table Name

`tTag`, `tTagCompare`

### API Object Name

`DbTagCompareComposite`

### Entity Description

Compare Tags compare two Tags and calculate a Discrete result. Available comparison operations include equality, inequality, greater than, greater than or equal to, less than, and less than or equal to. You can define what values to return when the comparison returns True or False, using either constants or Tags.

## Properties

`Left Operand [ LeftTagID or LeftConstant ]`

Value of the left (first) operand for the comparison, which may be a constant or the value of another Tag. This setting's data type must match the Right Operand's data type.

`Operation [ Operation ] : ETS.Core.Enums.TagCompareOperation`

Comparison operation to perform on the Left and Right Operands. Select **=** (equal to), **<>** (not equal to), **>** (greater than), **>=** (greater than or equal to), **<** (less than), or **<=** (less than or equal to).

`Right Operand [ RightTagID or RightConstant ]`

Value of the right (second) operand for the comparison, which may be a constant or the value of another Tag. This setting's data type must match the Left Operand's data type.
