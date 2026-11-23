# UpdateVirtualTagByName

```csharp
Result<bool> UpdateVirtualTagByName<T>(int tagName, T value, [IUnitOfWork uow])
```

Updates a Virtual Tag returns a [Result](../../api-models-reference/api-models/result-t) object. The `tagName` identifies the Virtual Tag to be updated by Name. The `value` parameter is the new desired value of the Virtual Tag. The optional `uow` argument can be used to ensure that this update occurs as part of a transaction.

{% hint style="warning" %}
The Tag specified must be a `Virtual Tag` or the operation will fail.
{% endhint %}

## Examples

### Update a Virtual Tag by Name

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Provide a valid Tag Name (from tTag.Name)
    string tagName = "YourTagNameHere";
    // Provide the new Tag Value
    string tagValue = "1";

    // Add the transaction to the Unit of Work object
    this.Ets.Api.Tags.UpdateVirtualTagByName(tagName, tagValue, uow).ThrowIfFailed();

    // Execute the Unit of Work object and push the new Tag Value to the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
