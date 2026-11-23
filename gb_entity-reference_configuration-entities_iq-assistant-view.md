# IQ Assistant View

## Summary

### Entity Name

IQ Assistant View

### Database Table Name

`tIqAssistantView`

### API Object Name

`DbIqAssistantView`

### Entity Description

IQ Assistant Views provide SQL Server Views that are used by TrakSYS IQ to query the TrakSYS database and generate responses to prompts. These Views assist TrakSYS IQ in querying the correct information and help provide more meaningful responses based on the given prompt.

## Properties

`IqAssistantID`

Specifies the IQ Assistant associated with the configured Assistant View.

`ViewName`

Contains the Name provided for the configured Assistant View.

`ViewDescription`

Contains the description used for the Assistant View. TrakSYS may reference this description for additional context when using the View to query for a given prompt.

`ViewSql`

Specifies the SQL that will be used to query and return data based on the provided prompt.
