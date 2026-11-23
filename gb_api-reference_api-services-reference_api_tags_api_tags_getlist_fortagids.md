# ForTagIDs

```csharp
Dictionary<int, Tag> ForTagIDs(List<int> idList)
```

Returns a Dictionary of Tag IDs and Tag objects provided a List of Tag IDs.

## Examples

### Get a Dictionary of Tags by Tag ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create List to contain Tag IDs (from tTag.ID)
    List<int> tagList = new List<int>();
    // Get Datatable of tTag records
    string sql = @"SELECT TOP 10
                     ID
                   FROM
                     tTag";
    DataTable tagDataTable = this.Ets.Api.Util.Db.GetDataTable(sql).ThrowIfFailed();

    // Loop through the rows and transfer the IDs to the List
    foreach (DataRow row in tagDataTable.Rows)
    {
      tagList.Add(row.GetInteger("ID", -1));
    }

    // Get a Dictionary of Tag Objects by Tag ID
    var tagRecords = this.Ets.Api.Tags.GetList.ForTagIDs(tagList).ThrowIfNull("Failed to load Tag Objects.");

    // Tag properties can now be accessed for each row of the Dictionary
    foreach (var tagRecord in tagRecords)
    {
      // Access the Key Value Pair for each row in the Dictionary
      int tagID = tagRecord.Key;
      var tagObject = tagRecord.Value;

      // Write code to process each record...
    }
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
