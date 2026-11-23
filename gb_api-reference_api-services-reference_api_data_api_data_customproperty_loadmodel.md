# Load Model

```csharp
bool LoadModel(ICustomPropertyModel model)
```

This method retrieves the custom property values for the entity object passed in as the `model` argument. Db\[ENTITY] Model object passed in must implement the `ICustomPropertyModel` interface (the objects that can contain custom properties implement this interface). The entity object's `CustomProperties` Dictionary is populated with the loaded values.

This method returns a `bool` result indicating the success or failure of the load operation.

## Examples

### Load Material Custom Properties

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide additional values or IDs for use with the query as needed
    // A value of 2 for a Material Version State means it is an active Material
    int versionState = 2;
    // Create query to retrieve Material records and include any additional values or IDs
    string sql = @"SELECT TOP 5 
                      * 
                   FROM 
                      tMaterial 
                   WHERE 
                      VersionState = {0} 
                   ORDER BY 
                      ID DESC".FormatWith(versionState.AsString());
    // Get list of DbMaterial Model Objects based on query results
    var material = this.Ets.Api.Data.DbMaterial.GetList.WithSql(sql).ThrowIfLoadFailed("VersionState", versionState);
    // Iterate through each DbMaterial object in the list
    foreach (var mat in material)
    {
      // Load the Custom Properties for the entity
      this.Ets.Api.Data.CustomProperty.LoadModel(mat);
      // Access the Custom Properties by full key
      string customPropertyValue = mat.CustomProperties.GetAsString("CPScheme.CPFullKey", "");
      // Additional custom code...
    }
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
