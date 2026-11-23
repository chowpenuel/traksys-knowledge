# Event VTR

## Summary

### Entity Name

Event VTR

### Database Table Name

`tEventVtr`

### API Object Name

`DbEventVtr`

### Entity Description

Each row in this table represents a tag value (VTR) that has been recorded at the start or end of a specific Event.

## Properties

`EventID`

The unique identifier (primary key) for the parent Event that represents the actual causal or highest priority Event Definition in progress at the time.

`EventVtrDefinitionID`

The unique identifier (primary key) for the Event VTR Definition which caused the Tag value to be captured by TrakSYS.

`TagValue`

The value of the Tag that was recorded at the Event start or end.

`EventEdgeType : ETS.Core.Enums.EventEdgeType`

This is an enumeration representing the Event edge at which TrakSYS records the VTR. Possible values are:

* **Start** = 0
* **End** = 1
