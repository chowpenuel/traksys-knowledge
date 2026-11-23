# IQ Assistant Lookup

## Summary

### Entity Name

IQ Assistant Lookup

### Database Table Name

`tIqAssistantLookup`

### API Object Name

`DbIqAssistantLookup`

### Entity Description

IQ Assistant lookups provide a way to map raw values to human-readable values. For example, when submitting a prompt using TrakSYS IQ asking for System information, the response may contain the System ID when returning the results. An IQ Assistant Lookup can be created to provide an alias mapped to System Name when the System ID is returned. This value will be displayed to the user in the response instead of the System ID

## Properties

`IqAssistantID`

Specifies the IQ Assistant associated with the current Lookup.

`Lookup Column Name [ LookupName ]`

Specifies the column name that may appear in IQ Assistant Views. TrakSYS IQ uses this value when querying information related to the original prompt.

`Key Field Name [ KeyFieldName ]`

Provides the aliased name that will be returned for a given Lookup Column Name.

`Description Field Name [ DescriptionFieldName ]`

Provides a description for the field when returning data. TrakSYS IQ may use this information when determining which columns should be returned based on the orginal prompt.

`SQL [ LookupSql ]`

Specifies the SQL that will be used to return the Key and Description combination, which aid in contextualizing the Lookup Column Name from IQ Assistant Views.
