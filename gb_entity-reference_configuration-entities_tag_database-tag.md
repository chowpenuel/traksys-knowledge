# Database Tag

## Summary

### Entity Name

Database Tag

### Database Table Name

`tTag`, `tTagOleDb`

### API Object Name

`DbTagOleDbComposite`

### Entity Description

Database Tags obtain their value from an OLE DB source, such as a Microsoft SQL Server database. Database Tags use their Access Names to query the OLE DB data source for data, and then return a single value from the result set.

A Database Tag obtains its value from a single Value Column in the result set. For result sets with multiple rows, you can specify a Key Column and Key Value to isolate a specific row using any unique, identifying key.

## Properties

`Value Column Name [ ValueColumnName ]`

The name of the Column in the result set returned by the Database Access Name to use for this Tag's value.

`Use Key Column [ UseKeyColumn ]`

For result sets with multiple rows, set this to True to specify a Key Column Name which uniquely identifies each row and then specify a Key Column Value to select a row to use for this Tag's value.

`Key Column Name [ KeyColumnName ]`

Name of a Column which uniquely identifies each row. Use this setting in combination with Key Column Value to isolate a single row from a result set with multiple rows. For example, if the OLE DB query returns a result set with an ID column uniquely identifying each row, set this property to "ID" and then set Key Column Value to the ID of the row you would like to use for this Tag's value. Use Key Column must be True for this setting to take effect.

`Key Column Data Type [ KeyColumnDataType ]`

The data type of the Column specified by Key Column Name. For example, if your Key Column Name specifies an integer ID column, this setting should be Integer. Value options are String, Integer, Float, and Discrete.

`Key Column Value [ KeyColumnValue ]`

The key value to isolate a single row in a result set which may contain multiple rows. Use Key Column Name to specify which column represents the result set's keys. The Logic Service will scan the OLE DB result set for a row with this value in the column specified by Key Column Name, and then return the value in the column specified by Value Column Name.

For example, if your result set has an ID column uniquely identifying each row, set Key Column Name to "ID" and set Key Column Value to the appropriate ID, such as 5, to narrow the results to a single row; the Logic Service will then set the value of this Tag according to the column specified by Value Column Name.
