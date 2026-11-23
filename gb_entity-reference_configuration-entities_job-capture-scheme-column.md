# Job Capture Scheme Column

## Summary

### Entity Name

Job Capture Scheme Column

### Database Table Name

`tJobCaptureSchemeColumn`

### API Object Name

`DbJobCaptureSchemeColumn`

### Entity Description

This entity defines a Data Type and capture behavior for a specific column in the Job Capture Scheme.

## Properties

`Job Capture Scheme [ JobCaptureSchemeID ]`

Specifies the parent Job Capture Scheme

`Data Type [ DataType ] : ETS.Core.Enums.DataType`

The data type for the Column.

`Capture Value On [ JobCaptureOnType ] : ETS.Core.Enums.JobCaptureOnType`

The time at which the Logic Service should record the associated Capture Tags' values. Select "Job Start" for the Logic Service to record the Capture Tags' values when a Job starts, or select "Job End" for the Logic Service to record the Capture Tags' values when a job ends. If "Job Record Creation" is selected, data captures is done only on the initial Job start, but not on successive Job restarts. If N/A is selected no data capture is performed.

* **None** = 0
* **JobRecordCreation** = 1
* **JobActivation** = 2
* **JobDeactivation** = 3

`Column Key [ ColumnKey ]`

A string indicating the column number (values `01` - `10`).
