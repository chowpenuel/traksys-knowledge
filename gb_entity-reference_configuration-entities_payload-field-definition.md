# Payload Field Definition

## Summary

### Entity Name

Payload Field Definition

### Database Table Name

`tPayloadFieldDefinition`

### API Object Name

`DbPayloadFieldDefinition`

### Entity Description

A Payload Field Definition describes a data field within a given Payload Definition.

## Properties

`Payload Field Definition Type [ PayloadFieldDefinitionType ]`

A Payload Field Definition Type categorizing this Payload Field Definition (solely for organizational and reporting purposes).

`Source Path [ SourcePath ]`

Specifies the path at which the data will be found.

For example given the jobID element in the following XML:

```xml
<root>
    <jobID></jobID>
</root>
```

The Source Path should be set as `jobID`.

{% hint style="warning" %}
If the Source Path is left blank, data for this Payload Field Definition will not be returned when converting to a Model or sent out when converting back to Payload.

By design, a Source Path is not required for extensibility purposes. The Payload Field Definition can still be populated in a Payload Definition Script Class.
{% endhint %}

`Parent Payload Deifnition ID [ ParentPayloadDeifnitionID ]`

Specifies the parent entity in the configuration hierarchy.

`Data Type [ DataType ] : ETS.Core.Enums.ConnectDataType`

The data type for the value. Possible values are:

* **Object** = 0
* **String** = 1
* **Integer** = 2
* **Double** = 3
* **Boolean** = 4
* **DateTime** = 5
* **DateTimeOffset** = 6
* **Enum** = 7
* **Long** = 8

`Default Value [ DefaultValue ]`

Specifies the default value that will appear in the entry field that will appear for this Payload Field Definition.

`Data Type Name [ DataTypeName ]`

Alternate Data Type Name (e.g. a custom enum) to be used instead of the Key for the generated class and definition name.

`Format String [ FormatString ]`

Specifies what format the data should be represented in.

`Is List [ IsList ]`

Specifies if the data is an individual item or a list. Note that the Data Type must be set to `Object` if `Is List` is true.

Note that the payload import option will automatically set this to true if it determines that the imported attribute should be treated as a list.

`Required Type [ RequiredType ]`

Specifies if the payload field definition is required.
