# WriteCritical

## Summary

```csharp
bool WriteCritical(string message, string category, string data)
```

This method creates an entry in the `tLogCustom` table of the `critical` type. The Message, Category, and Data fields are populated with the contents of the `message`, `category`, and `data` arguments.

This method always returns `false`.

## Examples

### Write a Critical Log Entry

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

  // If a single value is used, a simple string is recommended
  //var logDataString = "SystemID = {0}".FormatWith(sysID);

  // Provide a Log Data Array to provide additional logging information
  var logDataArray = new LogData[]
  {
    new LogData("SystemID", sysID),
    new LogData("ModuleTriggerKey", mtKey)
  };
  // If multiple values are used, using toJson() is recommended
  var logDataString = this.Ets.ToJson(logDataArray);

  try
  {
    // Check the existing Module Triggers
    var existingTriggerCount = this.Ets.Api.Util.Db.ExecuteScalar<int>("SELECT COUNT(ID) FROM tModuleTrigger WHERE TriggerKey = {0}".FormatWith(mtKey.ToSql())).ThrowIfFailed();
    // Provide Warning messages if other Module Trigger entries already exist
    if (existingTriggerCount > 0)
      this.Ets.Api.Util.LogCustom.WriteWarning("Pending Module Triggers exist for target Module.", logCategory, logDataString);

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

    // Write a Debug message stating that the Module Trigger is being created
    this.Ets.Api.Util.LogCustom.WriteDebug("Creating Module Trigger", logCategory, logDataString);
    // Insert the new Module Trigger entry into the database
    this.Ets.Api.Data.DbModuleTrigger.Save.InsertAsNew(mt).ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Write a Critical error message to the TrakSYS Log (tLog) if the process fails
    this.Ets.Api.Util.LogCustom.WriteCritical(ex.Message, logCategory, logDataString);
  }
}
```
