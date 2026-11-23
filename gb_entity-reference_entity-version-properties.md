# Entity Version Properties

Several entities (Product, Material and Recipe) contain a set of fields which enable the storage of version history within the database table. As new versions of the entity are defined, old versions remain in the table as historical record. The following common fields exist for each entity table that supports versions.

## Properties

`Version`

Specifies the version of the entity record.

`VersionENTITY [ VersionENTITYID ]`

Specifies the `ID` of current active entity in the chain. The current active entity will always have the `VersionENTITYID` field equal to its own `ID`. All historical entities in a chain will always have the same `VersionENTITYID` value.

`Version State [ VersionState ] : ETS.Core.Enums.VersionState`

Specifies the current state of the entity version. Possible values are:

* **Draft** = 1
* **Active** = 2
* **Retired** = 3

`Version Activated Date/Time [ VersionActivatedDateTime ]`

Stores the Date/Time when the entity moves into the Active Version State.

`Version Activated User [ VersionActivatedUser ]`

Stores the User (login) who has moved the entity into the Active Version State.

`Version Activated Notes [ VersionActivatedNotes ]`

Stores the optional Notes when the entity is moved into the Active Version State.

`Version Retired Date/Time [ VersionRetiredDateTime ]`

Stores the Date/Time when the entity moves into the Retired Version State.

`Version Retired User [ VersionRetiredUser ]`

Stores the User (login) who has moved the entity into the Retired Version State.

`Version Retired Notes [ VersionRetiredNotes ]`

Stores the optional Notes when the entity is moved into the Retired Version State.

`Version Approval Date Time [ VersionApprovalDateTime ]`

Stores the Date/Time of when the entity Version was approved.

`Version Approval User [ VersionApprovalUser ]`

Stores the User who approved the Version.

`Version Approval Notes [ VersionApprovalNotes ]`

Stores the optional Notes when a Version is approved.

`Version Obsolete Date Time [ VersionObsoleteDateTime ]`

Stores the Date/Time of when the entity Version was marked as Obsolete.

`Version Obsolete User [ VersionObsoleteUser ]`

Stores the User who approved to mark the Version as Obsolete.

`Version Obsolete Notes [ VersionObsoleteNotes ]`

Stores the optional Notes when a Version is marked as Obsolete.
