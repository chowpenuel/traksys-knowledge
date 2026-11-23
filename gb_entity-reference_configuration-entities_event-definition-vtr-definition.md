# Event Definition VTR Definition

## Summary

### Entity Name

Event Definition VTR Definition

### Database Table Name

`tEventVtrDefinition`

### API Object Name

`DbEventVtrDefinition`

### Entity Description

Event Definition VTR (Value-To-Record) Definitions specify supplementary Tag Values to record when an Event starts or ends. This entity serves to store configuration for VTRs against individual Event Definitions, as well as at the System level. A System level VTR Definition will have a NULL value for the EventDefinitionID field. VTRs defined at the System level will be captured whenever ANY Event under that System starts or ends.

## Properties

`System [ SystemID ]`

Specifics the parent System.

`Event Definition [ EventDefinitionID ]`

Specifics the parent Event Definition.

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the value.

`Record Tag [ RecordTagID ]`

Tag whose value the Logic Service should when the Event starts or ends.

`Event Edge [ EventEdgeType ] : ETS.Core.Enums.EventEdgeType`

The time at which the Logic Service should record the VTR. Select "Event Start" for the Logic Service to record the VTR when an Event starts, or select "Event End" for the Logic Service to record the VTR when an Event ends.

* **Start** = 0
* **End** = 1
