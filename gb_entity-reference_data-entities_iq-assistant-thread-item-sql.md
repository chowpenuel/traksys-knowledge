# IQ Assistant Thread Item SQL

## Summary

### Entity Name

IQ Assistant Thread Item SQL

### Database Table Name

`tIqAssistantThreadItemSql`

### API Object Name

`DbIqAssistantThreadItemSql`

### Entity Description

IQ Assistant Thread Item SQL entities contain the exact SQL queries used to generate a response to a given prompt. Prompts that do not require SQL queries will not have a Thread Item SQL record.

## Properties

`IqAssistantThreadItemID`

Specifies the parent IQ Assistant Thread Item associated with the current IQ Assistant Thread Item SQL record.

`Sql`

Contains the exact SQL query used to generate a response to a given prompt.

`IsSuccess`

Contains a Boolean value that determines whether the SQL execution was successful. A Boolean value of 1 (or True) means the execution was successful which a value of 0 (or False) means it was not successful.

`DataJson`

Contains a Json result of the data that was pulled from the TrakSYS database to answer the initial prompt. If no query was needed to answer the prompt, then this field will contain no data.

`ErrorMessage`

Contains the text of the error message for an attempted SQL execution. This field will be populated if TrakSYS IQ encounters any issues while attempting to execute the SQL statement to generate the response.

`FailedIqAssistantThreadItemSqlID`

Specifies the parent IQ Assistant Thread Item SQL record used for the SQL retry. This field is used when the initial query execution fails and TrakSYS IQ makes additional attempts to execute the same SQL statement.
