# ConnectionInfo

The `ConnectionInfo` object holds various information on how an external application should connect to TrakSYS using the API.

## Properties

`string ApplicationName`

Represents what the name of the custom External Application is. This is the source for the Application field in the Log entries, as well as helping troubleshoot issues with SQL Trace.

`int CommandTimeout = -1`

The time in seconds to wait for the command to execute. If 0 is specified, then no timeout will occur. If -1 is specified, then it will use the default determined by the .NET Framework.

`int ConnectTimeout = 30`

The time in seconds to wait while trying to establish a connection before terminating the attempt and generating an error. If 0 is specified, then no timeout will occur.

`string Login = "edbApp"`

The Database Login to use to be used when connecting to the SQL Server Database. This value is effectively ignored if `UsesWindowsAuthentication` is `true`.

`string Name = "EDB"`

The Name of the Database to be used when connecting to SQL Server.

`string Password`

The Database password, used with Login, to provide the security credentials for connecting to the SQL Server Database. This value is effectively ignored if `UsesWindowsAuthentication` is `true`.

`string Server = "(local)"`

The name or network address of the instance of SQL Server to connect to.

`string Template`

This represents a token-able `string` that will be used to build the ConnectionString for use when connecting to SQL Server. Available tokens to be replaced are `{databaseServer}`, `{databaseName}`, `{databaseLogin}`, `{databasePassword}`, `{integratedSecurity}`, `{connectTimeout}`, `{appName}`.

`bool UsesWindowsAuthentication = false`

Indicates whether the `Login` and `Password` are specified in the connection (when `false`) or whether the current Windows account credentials are used for authentication (when `true`).
