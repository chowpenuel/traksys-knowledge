# CheckConnection

```csharp
Result CheckConnection()
```

This method checks if the connection information contained in the current instantiated API object is able to establish a connection with the database.

This method returns a [Result](../../../api-models-reference/api-models/result-t) object with error messages (if any), and a success `boolean` (`true` if the connection succeeded, `false` if it did not).

## Examples

### Check API Database Connection after Load

After getting a new instance of the API (see Accessing the API from an [External Application](../../../accessing-api/external-application)), the connection can be checked:

```csharp
// check if the connection information is correct
api.Util.Db.CheckConnection().ThrowIfFailed();
```
