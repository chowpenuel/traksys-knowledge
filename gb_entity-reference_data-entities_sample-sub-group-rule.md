# Sample Sub-Group Rule

## Summary

### Entity Name

Sample Sub Group Rule

### Database Table Name

`tSampleSubGroupRule`

### API Object Name

`DbSampleSubGroupRule`

### Entity Description

Each record in this table represents each time a Rule Violation that has been triggered on a Sample Sub-Group.

## Properties

`SampleSubGroupID`

The unique identifier (primary key) of the Sample Sub-Group which has violated a Sample Definition Rule Definition.

`SampleDefinitionRuleDefinitionID`

The unique identifier (primary key) of the Sample Definition Rule Definition which this Sample Sub-Group has violated.

`User`

This field can be used to record the User who has reviewed the Rule violation occurrence.

`Notes`

The field can be used to record any notes made by a User who has reviewed the Rule violation occurrence.
