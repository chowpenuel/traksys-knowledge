# ByID

```csharp
Tag ByID(int id)
```

This method loads a Tag object with the Tag ID specified by the `id` argument.

This method returns an object of type [Tag](../../../api-models-reference/api-models/tags/tag).

## Examples

### Load a Tag by ID

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Tag ID (from tTag.ID)
    int tagID = -1;
    // Load the Tag object by Tag ID
    var tagObject = this.Ets.Api.Tags.Load.ByID(tagID).ThrowIfLoadFailed("TagID", tagID);

    // Tag properties can now be accessed through the object
    // For example:
    string tagValue = tagObject.Value;
    string tagName = tagObject.Name;
    // etc...

    // Continue using the Tag Object in code as needed...
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
