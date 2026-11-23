# IQ Assistant View Column

### Entity Name

IQ Assistant View Column

### Database Table Name

`tIqAssistantViewColumn`

### API Object Name

`DbIqAssistantViewColumn`

### Entity Description

IQ Assistant Columns assist in mapping the individual columns for a given Assistant View. These columns will contain raw data values (such as System IDs) or human-readable values (such as System Name). IQ Assistant Lookups can be used to map human-readable values for columns that return raw data values.

## Properties

`IqAssistantViewID`

Specifies the Assistant View associated with the configured Assistant View Column.

`ColumnName`

Contains the column name for the Assistant View. This value is automatically generated based on the query provided for the Assistant View.

`ColumnDataType`

Specifies the Data Type used for the current View Column.

`ColumnType`

Contains an Enumeration value that determines the column data type.

`ColumnVariablesJson`

Contains a Json list of variables included with the View Column. This is used for additional context when TrakSYS IQ generates responses for prompts.
