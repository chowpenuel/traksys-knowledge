# Template

## Summary

### Entity Name

Template

### Database Table Name

`tTemplate`

### API Object Name

`DbTemplate`

### Entity Description

A Template represents a versioned package of configuration or content that can be imported and applied within the system. Templates are used to store serialized content along with identifying and versioning metadata.

## Properties

`Key GUID [ KeyGuid ]`

Specifies a globally unique identifier used to identify the Template across systems and deployments.

`Source GUID [ SourceGuid ]`

Specifies the globally unique identifier of the source Template from which this Template originated. This field is used to track lineage across exports and imports.

`Version [ Version ]`

Specifies the version label associated with the Template.

`Version Auto [ VersionAuto ]`

Specifies an automatically incremented version value used for internal version tracking.

`Content [ Content ]`

Contains the serialized content of the Template.

`Import Date/Time [ ImportDateTime ]`

Specifies the date and time when the Template was imported into the system.
