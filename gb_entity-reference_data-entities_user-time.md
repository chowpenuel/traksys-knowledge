# User Time

## Summary

### Entity Name

User Time

### Database Table Name

`tUserTime`

### API Object Name

`DbUserTime`

### Entity Description

Each row of this table represents a user-session which is typically used to keep track of Operators via their unique log-in on a specific System. While there is no built-in dashboard which writes to this table, the API object (DbUserTime) can be used in script to log these user sessions.

## Properties

`UserID`

Specifies the unique identifier (primary key) of the logged-in User.

`SystemID`

Specifies the unique identifier (primary key) of the System which the User has logged-in to.

`StartDateTime`

Specifies the Start date and time of this User's session, or when they logged-in.

`EndDateTime`

Specifies the End date and time of this User's session, or when they logged-out. NULL if the User is still currently logged-in.

`ShiftHistoryID`

The unique identifier (primary key) for the Shift (Shift History record) that was in progress when the User logged-in.

`Notes`

Contains any notes added from the log-in and log-out user interfaces.

`Capture01–10`

The Capture01 to 10 values are custom-defined fields which can be recorded either when the User logs in or out. Examples include what machine they were manning, etc.
