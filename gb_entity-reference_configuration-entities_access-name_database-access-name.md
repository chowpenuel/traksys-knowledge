# Database Access Name

## Summary

### Entity Name

Database Access Name

### Database Table Name

`tAccessName` + `tAccessNameOleDb`

### API Object Name

`DbAccessNameOleDbComposite`

### Entity Description

A Database Access Name defines a connection to an OLEDB relational data source via a query that returns a data table. Any Database Tags that are related to an Database Access Name will use its connection to receive value updates.

## Properties

`Connection String [ ConnectionString ]`

An OLEDB connection string specifying how to connect to the database. This string should include the provider, initial catalog, data source, and security information.

`Query Interval Seconds [ IntervalSeconds ]`

The delay Logic Service will wait before re-executing the specified Query. This interval determines how frequently the Logic Service updates Database Tag values for this Access Name.

`Query Timeout Seconds [ TimeoutSeconds ]`

Limit on how long the Logic Service will wait for the specified Query to complete. If the Query times out, all dependent Database Tags will have bad Quality.

`Query [ Query ]`

SQL query string for retrieving the desired data from the OLEDB connection. The query must conform to the rules and syntax of the query language used by the data source.
