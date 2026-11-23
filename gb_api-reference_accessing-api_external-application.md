# External Application

This sample describes the initialization and instantiation of the top level API service. This service is used to perform all API operations. Note that the TrakSYS API can only be used when properly licensed (included on all Professional and higher packages).

The API uses the database connection string information that is stored in the TrakSYS `connection.config` file on the local computer. If the API is being used on a computer where there are no other TrakSYS components installed, the connection string information must be specified manually when the API object is created.

The API is contained in the TrakSYS **Core.Api.DLL** file which can be found in the **Program Files\Parsec\TrakSYS** directory. This is a standard .NET assembly and must be included in the external application in order to be used.

## Examples

```csharp
// set the connection info (only required when the API code is NOT running on a machine with TrakSYS components installed)
var ci = new ETS.Core.Api.Models.ConnectionInfo();
 ci.ApplicationName = "APPNAME";
 ci.Server = "SERVERNAME";
 ci.Name = "DATABASENAME";
 ci.Login = "edbApp";
 ci.Password = "Sqlapp!23";
 ci.UsesWindowsAuthentication = false;

var api = ETS.Core.Api.ApiService.StartupNewApplicationWithConnectionSettings(ci);

// The API object can now be used
```
