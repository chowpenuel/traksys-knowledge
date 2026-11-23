# Job System Planned

## Summary

### Entity Name

Job System Planned

### Database Table Name

`tJobSystemPlanned`

### API Object Name

`DbJobSystemPlanned`

### Entity Description

Each row in this table represents the intended System on which a Job is to be executed. Multiple records may exist for the same Job if that Job is able to run on different Systems.

## Properties

`JobID`

Identifies the Job to be executed.

`SystemID`

Identifies the System on which the Job is to be executed.

`Attribute01 -10`

The Attribute01 to 10 value fields are used for extensibility. There are currently no built-in mechanisms for populating these fields. They can be used to store any type of data related to the Job.
