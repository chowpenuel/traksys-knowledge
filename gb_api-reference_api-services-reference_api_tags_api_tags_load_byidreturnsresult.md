# ByIDReturnsResult

```csharp
Result<Tag> ByIDReturnsResult(int id)
```

This method loads a Tag object with the Tag ID specified by the `id` argument.

This method returns a [Result](../../../api-models-reference/api-models/result-t) object containing error messages (if any), and whether or not the call was successful.

{% hint style="warning" %}
This method is primarily used to address scenarios where additional custom validation must be performed. In a vast majority of cases, it is recommended to use the [`ByID()`](byid) method in combination with the TrakSYS-specific [Extension Methods](../../../../tsweb/scripting/extension-methods) (such as `ThrowIfFailed()` and `ThrowIfLoadFailed()`).
{% endhint %}

## Examples

### Load a Tag by ID

This example was created within the page script of a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes). The different ways to access the TrakSYS API within each area of the application can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Instantiating-the-API-Service).

```csharp
// Provide a valid Tag ID (from tTag.ID)
int tagID = -1;
// Load the Tag object by Tag ID
var result = this.Ets.Api.Tags.Load.ByIDReturnsResult(tagID);

// Add a condition to check the result and perform additional logic
// depending on whether data is returned
if (result.Return == null)
{
  // Add custom code to handle scenarios where a tag fails to load
  // or add additional custom error handling as shown below
  this.Ets.Debug.FailFromResultMessages(result.Messages);
  this.Ets.Api.Util.LogCustom.WriteErrorsFromResultObject(result, "Tag Load Failure");
}

// Tag properties can now be accessed through the object
// For example:
//string tagValue = result.Return.Value;
//string tagName = result.Return.Name;
// etc...

// Continue using the Tag Object in code as needed...
```
