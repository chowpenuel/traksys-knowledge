# SQL Module Step

## Summary

### Entity Name

SQL Module Step

### Database Table Name

`tModuleStepSql`

### API Object Name

`DbModuleStepSql`

### Entity Description

The SQL Module Step allows the execution of SQL statements against a specified relational data source within a Data Management Service.

## Properties

`Module Step [ ModuleStepID ]`

Specifies the parent Module Step.

`Parameter Connection String [ ParameterConnectionStringContent ]`

The OLEDB connection string used when executing the `Parameter SQL`. A blank value is the default and specifies a connection to the local TrakSYS database.

`Parameter Command Timeout [ ParameterCommandTimeout ]`

The command timeout used when executing the `Parameter SQL`. A value of 0 represents an unlimited timeout.

`Parameter SQL [ ParameterSqlContent ]`

A SQL `SELECT` statement that retrieves and calculates data from a relational data source. The result set from the `Parameter SQL` is passed to the `Execute SQL` specified below.

`Execute Connection String [ ExecuteConnectionStringContent ]`

The OLEDB connection string used when executing the `Execute SQL`. A blank value is the default and specifies a connection to the local TrakSYS database.

`Execute Command Timeout [ ExecuteCommandTimeout ]`

The command timeout used when executing the `Execute SQL`. A value of 0 represents an unlimited timeout.

`Execute SQL [ ExecuteSqlContent ]`

A SQL action (`INSERT`, `UPDATE`, `DELETE`) statement that is executed once for each row in the result set returned by the `Parameter SQL`.
