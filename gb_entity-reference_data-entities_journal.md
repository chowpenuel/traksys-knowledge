# Journal

## Summary

### Entity Name

Journal

### Database Table Name

`tJournal`

### API Object Name

`DbJournal`

### Entity Description

Each row in this table represents a Journal entry created via a Journal entry user interface. Journals are often used to document different steps throughout a manufacturing process for record-keeping and to help document and improve procedures.

## Properties

`ParentJournalID`

Specifies the Journal ID of the parent Journal record. This is used for references to nested Journal entries.

`JournalDateTime`

The date and time the Journal was created.

`AreaID`

Identifies the Area associated with the Journal entry.

`SystemID`

Identifies the System associated with the Journal entry.

`JournalCategoryID`

Identifies the Journal Category this Journal entry was classified as.

`ShiftHistoryID`

Identifies the Shift History associated with the Journal entry.

`JobID`

Identifies the Job associated with the Journal entry.

`BatchID`

Identifies the Batch associated with the Journal entry.

`TaskID`

Identifies the Task associated with the Journal entry.

`Case`

An optional string field which can be used to later group, or create threads of Journal entries.

`Measure`

An optional numerical field which can be used to record a specific value as part of a Journal entry. For example, over time, this measurement can be displayed on a Journal user interface as a trend chart.

`Title`

Specifies a title for the current Journal entry.
