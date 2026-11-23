# Entity Reference Conventions

The following sections describe the general layout of each TrakSYS entity documentation page.

## Configuration vs. Data Entities

In general TrakSYS entities fall into one of two categories. **Configuration Entities** (and tables) are used to describe how TrakSYS is setup, and what business rules it is expected to execute. **Data Entities** (and tables) are used to store real-time and historical information collected from a implementation process.

## Entity Header

At the top of each entity reference page, the following information is conveyed.

### Entity Name

The name commonly used when this entity is listed in the TrakSYS user interface. Depending on the context, there may be several versions of this name used throughout the application, particularly in interfaces where space is a premium (an abbreviated version of this name may be displayed).

### Database Table Name

The related table name from the TrakSYS database.

### API Object Name

The related Db model object from the TrakSYS API. This object will be located in the `ETS.Core.Api.Data` namespace.

### Entity Description

A short description of the entity and its use within TrakSYS.

## Entity Properties

The entity reference page will list each property and its description in the following format...

`Property Name [ Database/API Field Name ]`

A short description of the property and its use within TrakSYS.
