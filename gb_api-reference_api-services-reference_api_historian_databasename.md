# DatabaseName

```csharp
string DatabaseName
```

Returns a string containing the TrakSYS Historian Database Name.

## Examples

### Retrieve the Historian Database Name

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Get the Historian Database Name
    // This is typically the TrakSYS Database Name with "_Historian" appended as a suffix
    string historianDbName = this.Ets.Api.Historian.DatabaseName;

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
