# Production Scheduling Stage Job

## Summary

### Entity Name

Production Scheduling Stage Job

### Database Table Name

`tPsStageJob`

### API Object Name

`DbPsStageJob`

### Entity Description

Each row in this table represents a Production Scheduling staged Job.

## Properties

`Production Scheduling Stage ID [ PsStageID ]`

The unique identifier of the Production Scheduling Stage under which the Job is staged.

`Start Date/Time [ StartDateTime ]`

The start datetime of the Production Scheduling staged Job.

`Duration Seconds [ DurationSeconds ]`

The planned duration of the staged Job in seconds.

`Padding Pre Seconds [ PaddingPreSeconds ]`

Associated time that will be assigned before a Job.

`Padding Post Seconds [ PaddingPostSeconds ]`

Associated time that will be assigned after a Job.

`Gap Pre Seconds [ GapPreSeconds ]`

Unassociated time that will be reserved before a Job.

`Gap Post Seconds [ GapPostSeconds ]`

Unassociated time that will be reserved after a Job.

`Changeover Pre Seconds [ ChangeoverPreSeconds ]`

The configured changeover time based upon the changeover type associated with the current Job and the previous Job.

`Changeover Post Seconds [ ChangeoverPostSeconds ]`

The configured changeover time based upon the changeover type associated with the current Job and the following Job.
