# Database Access Name Parameter

## Summary

### Entity Name

Database Access Name Parameter

### Database Table Name

`tAccessNameOleDbParameter`

### API Object Name

`DbAccessNameOleDbParameter`

### Entity Description

A Database Access Name Parameter specifies a Tag value that can be passed into a query for use in the SQL statement.

## Properties

`Name [ Parameter ]`

The unique name given to the parameter. The "@" character is automatically added to the front of the Parameter Name after you enter it. For example, if the parameter in a SQL Server query is named "@Param", the Name property for the parameter can be entered as "Param" without the "@".

`Access Name [ AccessNameID ]`

Specifies the parent entity in the configuration hierarchy.

`Tag [ ValueTagID ]`

The TrakSYS Tag containing the value to be passed in this parameter. This Tag may be of any type (OPC Tag, Virtual Tag, Compare Tag, etc.).

`Test Value [ TestValue ]`

A default value to use when executing the database query by clicking on the "Test Query" button. This is used in place of the current value for the Tag for testing and debugging purposes.
