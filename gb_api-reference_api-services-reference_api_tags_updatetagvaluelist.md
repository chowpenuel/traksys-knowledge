# UpdateTagValueList

```csharp
Result<bool> UpdateTagValueList(List<Tag> listOfTags, [IUnitOfWork uow])
```

This method allows a List of [ETS.Core.Api.Models.Tags.Tag](../../api-models-reference/api-models/tags/tag) objects passed in as the `listOfTags` argument, to be updated to the database at once. The optional `uow` argument can be used to ensure all Tags are updated as part of a transaction. See the [UnitOfWork](../../api-models-reference/unitofwork) object for examples of executing transactional API operations.

This method returns a [Result](../../api-models-reference/api-models/result-t) object containing error messages (if any), and whether or not the call was successful.

{% hint style="warning" %}
The Tags specified must be `Virtual Tags` or the operation will fail.
{% endhint %}

## Examples

### Update 2 Tags in one transaction

This example was created within a Button Click method for a Buttons Part on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
private void ButtonClick(object sender, EventArgs e)
{
  try
  {
    // Create a Unit of Work object
    var uow = this.Ets.Api.CreateUnitOfWork();
    // Provide valid Tag IDs (from tTag.ID)
    int firstTagID = -1;
    int secondTagID = -1;
    // Create List to contain Tag Objects
    var tagsList = new List<ETS.Core.Api.Models.Tags.Tag>();

    // Load Tag Objects as needed
    var firstTag = this.Ets.Api.Tags.Load.ByID(firstTagID).ThrowIfLoadFailed("TagID", firstTagID);
    var secondTag = this.Ets.Api.Tags.Load.ByID(secondTagID).ThrowIfLoadFailed("TagID", secondTagID);
    
    // Provide Tag Values
    firstTag.Value = "1";
    secondTag.Value = "0";
    
    // Add the Tag Objects to the List
    tagsList.Add(firstTag);
    tagsList.Add(secondTag);

    // Add the transactions to the Unit of Work object
    this.Ets.Api.Tags.UpdateTagValueList(tagsList, uow).ThrowIfFailed();

    // Push the new Tag Values to the database
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
  }
  catch (Exception ex)
  {
    // Throw error messages if the process fails
    this.Ets.Debug.FailFromException(ex);
  }
}
```
