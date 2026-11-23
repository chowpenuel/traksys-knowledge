# WriteError

## Summary

```csharp
bool WriteError(string message, string category, [LogData logArray])
```

This method creates an entry in the `tLog` table of the `error` type. The Message and Category fields are populated with the contents of the `message` and `category` arguments.

This method always returns `false`.

{% hint style="success" %}
While this method can be used to write custom Error messages to tLog, it is recommended to use a method under the `Api.Util.LogCustom` namespace instead (if possible). The tLog table is also populated with system messages from the TrakSYS Services and other parts of the software. The combination of system generated messages and custom messages can flood the tLog file and make it more difficult to find specific entries.
{% endhint %}

## Examples

### Write an Error entry

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  // Retrieve a valid Module Trigger Key 
  var mtKey = "ModuleTriggerKey";
  // Get the current System ID (from tSystem.ID)
  var sysID = this.Ets.Form.GetValueAsIntByKey("SystemID", -1);

  // Provide a Category. This is user-defined and can be any value.
  var logCategory = "ModuleTrigger From Web";
  // Provide a Log Data Array to provide additional logging information
  var logDataArray = new LogData[]
  {
    new LogData("SystemID", sysID),
    new LogData("ModuleTriggerKey", mtKey)
  };

  try
  {
    // Check the existing Module Triggers
    var existingTriggerCount = this.Ets.Api.Util.Db.ExecuteScalar<int>("SELECT COUNT(ID) FROM tModuleTrigger WHERE TriggerKey = {0}".FormatWith(mtKey.ToSql())).ThrowIfFailed();
    // Provide Warning messages if other Module Trigger entries already exist
    if (existingTriggerCount > 0)
      this.Ets.Api.Util.Log.WriteWarning("Pending Module Triggers exist for target Module.", logCategory, 5 /*default warning level = 5*/, logDataArray);

    // Add parameters to the Module Trigger
    var mArgs = new Dictionary<string, string>();
    mArgs["TriggeringUser"] = this.Ets.User.Login;
    mArgs["SystemID"] = sysID.AsString();
    // Create a DbModuleTrigger Model Object
    var mt = this.Ets.Api.Data.DbModuleTrigger.Create.FromParentNone();
    // Populate the Model Object with values
    mt.TriggerKey = mtKey;
    mt.TriggerDateTime = this.Ets.SiteNow;
    mt.Args = this.Ets.ToJson(mArgs);
    // Etc...

    // Write an Informational message stating that the Module Trigger is being created
    this.Ets.Api.Util.Log.WriteInformation("Creating Module Trigger", logCategory, logDataArray);
    // Insert the new Module Trigger entry into the database
    this.Ets.Api.Data.DbModuleTrigger.Save.InsertAsNew(mt).ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Write an error message to the TrakSYS Log (tLog) if the process fails
    this.Ets.Api.Util.Log.WriteError(ex.Message, logCategory, logDataArray);
  }
}
```
