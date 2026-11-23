# Sample

## Summary

### Entity Name

Sample

### Database Table Name

`tSample`

### API Object Name

`DbSample`

### Entity Description

Each row in this table represents a single test value taken within a parent Sub-Group for a specific Sample Definition. For Variable type Sample Definitions, the Sample represents a measured value. For Attribute type Sample Definitions, the Sample represents the number of items found within the Sub-Group that correspond to a specific Sample Category.

## Properties

`SampleSubGroupID`

The unique ID (primary key) of the Sample Sub-Group parent record for this sample.

`Value`

The actual value of the sample collected and recorded for the parent Sample Definition. For Variable type Sample Definitions, this value is a measurement. For Attribute type Sample Definitions, this value is the number of pieces that match a specified Sample Category.

`SampleCategoryID`

The unique ID (primary key) of the Sample Category to be associated with this sample (used for Attribute type Sample Definitions).

`Capture01 - 10`

The Capture01 to 10 value fields are used for extensibility. There are no built-in mechanisms for populating these fields. They can be used to store any type of data related to the measurement.
