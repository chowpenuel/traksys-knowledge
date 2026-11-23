# Metric Calculator Module Step

## Summary

### Entity Name

Metric Calculator Module Step

### Database Table Name

`tModuleStepMetricCalculator`

### API Object Name

`DbModuleStepMetricCalculator`

### Entity Description

The Metric Calculator Module Step allows the execution of a predefined Metric Definition within a Data Management Service Module.

## Properties

`Module Step [ ModuleStepID ]`

Specifies the parent Module Step.

`Metric Definition [ MetricDefinitionID ]`

Specifies the Metric Definition to be executed when the Module Step is executed.

`Parameter SQL [ ParameterSqlContent ]`

A pre-SQL statement run before the main Custom SQL statement from the Metric Definition. The Metric Definition's Custom SQL statement is run for each row in the Parameter SQL result set. This allows a set of Systems or Areas or KPI Calculations to be selected and the Custom SQL to be executed and Metrics calculated and stored for each entity.

The Parameter SQL is always run against the TrakSYS database.
