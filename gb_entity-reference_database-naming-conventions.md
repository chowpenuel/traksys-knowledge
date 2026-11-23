# Database Naming Conventions

The following sections describe some of the naming and organizational conventions used within the TrakSYS database. A concerted effort has been made to name items clearly and consistently.

## Table Names

All TrakSYS table names are prefixed with a lower case "t". For example, the Area table is called `tArea`. Table names are designed to match very closely with the configuration entity names within the software. For example, the configuration for Event Definitions is stored in a table called `tEventDefinition`. Many to many relationship tables are typically named using both entity names that they join. For example the table that related Systems to Event Category Groups is called `tSystemEventCategoryGroup`.

## View Names

All TrakSYS view names are prefixed with a lower case "vw". For example, the data view for Event data is called `vwEvent`.

## Stored Procedure Names

All TrakSYS stored procedures are prefixed with a lower case "sp". For example, the procedure for retrieving the current version information from the TrakSYS database is called `spVersionInformation`.

## Foreign Key Column Names

Columns that reference the ID column in another table, are typically named `<Entity>ID`, where `<Entity>` is the name of the target table without the "t" prefix. For example, the `tSystem.AreaID` field references the `ID` column in `tArea`. In some cases, additional descriptive text may be added to the beginning of a column name. For example, within `tSystem`, there are many columns that reference rows in `tTag`, therefore the field names will be `ProductTagID`, `JobTagID`, `BatchTagID`, etc...

## ID Fields

Most TrakSYS tables contain a column called `ID`. When present, this is the Primary Key for the table and its value is therefore unique within the table.
