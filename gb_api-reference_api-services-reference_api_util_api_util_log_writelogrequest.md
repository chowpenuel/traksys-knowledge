# WriteLogRequest

## Summary

```csharp
void WriteLogRequest(string message, string category, LogType logtype, string location, string stackTrace, string host, IEnumerable<LogData> logDataList, [int warningLevel])
```

This method creates an entry in the `tLog` table. The `tLog.Message` and `tLog.Category` fields are populated with the contents of the `message` and `category` parameters. The `logtype` parameter specifies the type of message that will be recorded (i.e. `Error`, `Information`, or `Warning`). The `location` and `stackTrace` parameters populate the `tLog.Location` and `tLog.Stack Trace` fields of the log entry, respectively. The computer name for the log entry is specified with the `host` parameter. Extra logging information can be included in the `logDataList` parameter for further debugging purposes. The optional `warningLevel` parameter determines if the message will be entered in `tLog` depending on the value of `MinWarningLevel` in the TrakSYS Settings section of Installation Manager.

{% hint style="warning" %}
This method is primarily used in scenarios where providing highly detailed and extensive logging is required or when none of the other methods in the `Api.Util.Log` namespace satisfy implementation requirements. In most cases, it is recommended to use the other methods in the `Api.Util.Log` namespace to help simplify the logging process.
{% endhint %}

{% hint style="success" %}
While this method can be used to write custom log messages to tLog, it is recommended to use a method under the `Api.Util.LogCustom` namespace instead (if possible). The tLog table is also populated with system messages from the TrakSYS Services and other parts of the software. The combination of system generated messages and custom messages can flood the tLog file and make it more difficult to find specific entries.
{% endhint %}

## Examples

### Create a Custom Log Entry in tLog

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a Message. This could include variables and other objects for debugging purposes.
    var msg = "Verbose logging test.";
    // Provide a Category. This is user-defined and can be any value.
    var category = "Extended Logging Example";
    // Provide a Log Type. These are enumeration values under the ETS.Core.Enums.LogType namespace
    var logType = LogType.Information;
    // Provide a Location. This typically includes where the message originated,
    // such as the method name
    var location = "ButtonClick(object sender, EventArgs e)";
    // Provide a stack trace. This can include the full method hierarchy of where the message originated
    var stack = Environment.StackTrace;
    // Provide a Host name. This is typically the computer name of the TrakSYS Application Server.
    // However, the client host name can be used instead (for better troubleshooting) if needed
    var host = this.Ets.Api.Util.General.ComputerName;
    // Create a list to contain additional Log Data Entries
    var logData = new List<LogData> { new LogData("TriggeringUser", this.Ets.User.Login) };

    // Create the log entry
    this.Ets.Api.Util.Log.WriteLogRequest(msg, category, logType, location, stack, host, logData, 5 /*default warning level = 5*/ );
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
