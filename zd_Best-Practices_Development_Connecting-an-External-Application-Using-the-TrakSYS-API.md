# Connecting an External Application Using the TrakSYS API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6826847693459-Connecting-an-External-Application-Using-the-TrakSYS-API*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

TrakSYS supports the ability to allow external applications to connect to it. This is also true for implementations that require custom [TrakSYS Apps](https://portal.parsec-corp.com/hc/en-us/articles/360037580834-Extensibility). The TrakSYS API can be used by referencing the `Core.Api.dll` file located in the root TrakSYS directory under **...\Program Files (x86)\Parsec\TrakSYS** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec\TrakSYS** for TrakSYS 12. Once this file has been referenced, the following code can be used to connect to the installation:
    
    
    // set the connection info (only required when the API code is NOT running on a machine with TrakSYS components installed)
    var ci = new ETS.Core.Api.Models.ConnectionInfo();
    ci.ApplicationName = "APPNAME";
    ci.Server = "SERVERNAME";
    ci.Name = "DATABASENAME";
    ci.Login = "edbApp";
    ci.Password = "Sqlapp!23";
    ci.UsesWindowsAuthentication = false;
    
    var api = ETS.Core.Api.ApiService.StartupNewApplicationWithConnectionSettings(ci);
    
    // the api object can now be used
    
    

**Note** : The [StartupNewApplicationWithConnectionSettings()](https://docs.parsec-corp.com/api-reference/accessing-api/external-application) method should only be used on startup within external applications. Attempting to use it inside of the TrakSYS application can cause serious issues in the TrakSYS Web.
