# Global.Tags

The `Tags` object is a collection that contains the individual `Tag` objects that are loaded into Logic Service. A specific `Tag` in the collection can be referenced using the following syntax … `Global.Tags["tagname"]`.

{% hint style="warning" %}
The Tags collection should only contain the literal string name of the tag:

`Global.Tags["tagname"]`

Attempting to use variables or dynamic values is not guaranteed to work and can cause issues with script execution. For example, doing the following is **NOT** recommended:

`string tagNameVariable = "TagNameHere";`

`Global.Tags[tagNameVariable]`

The Tags collection also helps create the Prerequisite Tag entries for Script Tags, which are required when referencing other Tags in code. Dynamic values or variables prevent the creation of these records, which can cause Script Tag code execution issues.
{% endhint %}

Each `Tag` object in the collection is of type `ISourceCodeTag` and contains the following properties.

```csharp
int ID { get; }
```

Returns the ID of the Tag.

```csharp
string Name { get; }
```

Returns the name of the Tag.

```csharp
int ETS.Core.Enums.DataType { get; }
```

Returns the TrakSYS Tag data type. Possible values are String, Integer, Float or Discrete.

```csharp
int ETS.Core.Enums.TagType { get; }
```

Returns the TrakSYS Tag type for the Tag.

```csharp
int Quality { get; }
```

Returns the current Quality for the Tag. This property is typically used for OPC or other externally acquired Tags. A value of 192 is typically good where any other value is bad, however the actual Quality values are source dependent.

```csharp
string ValueString { get; }
```

Returns the current value of the Tag cast to a `string` data type.

```csharp
int ValueInteger { get; }
```

Returns the current value of the Tag cast to an `int` data type.

```csharp
double ValueDouble { get; }
```

Returns the current value of the Tag cast to a `double` data type.

```csharp
bool ValueBoolean { get; }
```

Returns the current value of the Tag cast to a `bool` data type.
