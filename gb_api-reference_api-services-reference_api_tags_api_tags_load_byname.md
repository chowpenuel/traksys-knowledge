# ByName

```csharp
Tag ByName(string name)
```

This method loads a Tag object with the Tag Name specified by the `name` argument.

This method returns an object of type [Tag](../../../api-models-reference/api-models/tags/tag).

## Examples

### Load a Tag by Name

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Provide a valid Tag Name (from tTag.Name)
    string tagName = "YourTagNameHere";
    // Load the Tag object by Tag Name
    var tagObject = this.Ets.Api.Tags.Load.ByName(tagName).ThrowIfLoadFailed("TagName", tagName);

    // Tag properties can now be accessed through the object
    // For example:
    string tagValue = tagObject.Value;
    int tagQuality = tagObject.Quality;
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
