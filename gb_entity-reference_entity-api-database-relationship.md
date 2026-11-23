# Entity API Database Relationship

## Entity Names

In most cases, a TrakSYS entity has a 1-to-1 relationship with a table from the TrakSYS database (and therefore an API `Db` model object). For example, the **Event Definition** entity matches up with the `tEventDefinition` table in the database (and therefore the `ETS.Core.Api.Models.Data.DbEventDefinition` model object).

In some cases, a forward facing application entity name has diverged from the original database naming. For example, the **KPI Calculation** entity matches up with the `tOeeCalculation` table in the database (and therefore the `ETS.Core.Api.Models.Data.DbOeeCalculation` model object).

## Entity Property Names

In most cases, the properties for each entity are related to the fields in the associated database table (and therefore the properties from the API Db model object). For example, the `Description` property from the **Event Definition** entity matches up to the `tEventDefinition.Description` field in the database (and therefore the `Description` property of the `ETS.Core.Api.Models.Data.DbEventDefinition` model object).

In some cases a forward-facing application entity property name has diverged from the original database naming. For example, the `Re-Connect While True` property from the **OPC Access Name** entity matches up with the `tAccessNameOpc.ReConnectTagID` field in the database (and therefore the `ReConnectTagID` property of the `ETS.Core.Api.Models.Data.DbAccessNameOpc` model object).
