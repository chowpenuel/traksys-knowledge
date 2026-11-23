# Metric Definition

## Summary

### Entity Name

Metric Definition

### Database Table Name

`tMetricDefinition`

### API Object Name

`DbMetricDefinition`

### Entity Description

A Metric Definition describes a structured way of calculating and aggregating one or more values for a specified type of TrakSYS entity on a periodic or manually triggered basis. The definition includes the specific types of values that will be stored, as well as the SQL queries used to retrieve and calculation the data. The results of a Metric Definition execution are stored in the `tMetric` table in the TrakSYS database.

## Properties

`Metric Scheme [ MetricSchemeID ]`

Specifies the Metric Scheme that this definition will utilize.

`Entity Type [ MetricEntityType ]`

Defines the type of entity that this Metric Definition is typically associated with. The Non option should be selected when the type of entity is not one of the other choices present in the list.

`Rollup Type [ PeriodicRollupType ]`

Specifies the period that the Metric data is aggregated over.

`Parameter SQL [ ParameterSqlContent ]`

A pre-SQL statement run before the main Custom SQL statement below. The Custom SQL statement below is run for each row in the parameter SQL result set. This allows a set of Systems or Areas or KPI Calculations to be selected and the Custom SQL to be executed and Metrics calculated and stored for each entity.

The parameter SQL is always run against the TrakSYS database.

`Custom Connection String [ CustomMetricConnectionStringContent ]`

The connection string that is used for the Custom SQL property below. A blank value in this field represents the default connection to the TrakSYS database.

`Custom Command Timeout [ CustomMetricCommandTimeout ]`

The command timeout (in seconds) used for the Custom SQL statement above. A value of 0 indicates an infinite timeout.

`Custom SQL [ CustomMetricSqlContent ]`

SQL that is executed for each row returned by the Parameter SQL defined above. The purpose of the Custom SQL is to retrieve and aggregate data that will be stored in the `tMetric` table. All return columns from this query should be named `Value01` through `Value20`. The return values will be automatically written to the applicable fields in the tMetric record.
