# ToArgsString

## Summary

```csharp
string ToArgsString(IDictionary<string,object> argsDict)
```

This method converts all the entries in the `argsDict` parameter to a valid args `string` that can be used to set the value of API DbObjects like `DbNotification.Args`. The method returns a delimited property=value `string`. The delimiter between each property=value set in the args `string` is a carriage return character.

## Examples

### Create an Args String for a Notification

```csharp
// create dictionary with args elements
var args = new Dictionary<string, object>();
args.Add("UserID", "1");
args.Add("UserName", "John");
```

```csharp
// create args string
string argsString = api.Util.General.ToArgsString(args);
// args string = "UserID=1 UserName=John
```

```csharp
// set to Args property
DbNotification n = new DbNotification();
n.Args = argsString;
```
