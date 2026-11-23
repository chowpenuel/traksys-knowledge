# Unit of Work

## Summary

The `UnitOfWork` object represents a coding pattern, that in this instance is used to represent a database transaction.

## Properties

`int CommandTimeout`

Gets or sets the `Command Timeout` to be used when executing each individual statement in the `UnitOfWork`. By default, this uses the current Applications configuration setting.

`string ConnectionString`

Gets or sets the database connection string that will be used to commit data to the database. By default, this uses the current Applications connection `string`.

`bool IsLoggingEnabled = true`

Gets or sets if any errors will use the default logging behavior of TrakSYS.

`[ReadOnly] string ErrorMessage`

This returns the result of the last execution. If no errors occurred it will be empty, otherwise it will contain the last known error message.
