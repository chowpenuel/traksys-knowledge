# GetTagHistoryDefinitionIDByTagID

```csharp
Result<int> GetTagHistoryDefinitionIDByTagID(int tagID)
```

Retrieves the Tag History Definition ID of the given `tagID`, often used with the `GetTagHistory` methods. The ID returned is wrapped in a result object.

## Examples

### Get the Tag History Definition ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Tag ID (from tTag.ID)
    int tagID = -1;

    // Get the Tag History Definition ID by Tag ID
    int tagHistoryDefID = this.Ets.Api.Historian.GetTagHistoryDefinitionIDByTagID(tagID).ThrowIfFailed();

    // The variable can be used in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails.
    this.Ets.Debug.FailFromException(ex);
  }
}
```
