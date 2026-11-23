# Enum Format

## Enum Format

When the Values Dictionary item specified by an expression is an integer representation of a TrakSYS enumeration (enum), a special format code can be specified to translate the integer value into the string representation of the enumeration. The format code `enum`, followed by the **full namespace and enum typename** will return the string representation.

For enums that are defined in TrakSYS script classes (like the Developer | Scripts | Web or Global user interfaces), the assembly name must be included in the expression syntax (see examples below). The assembly name for TrakSYS script is **`Ts.Scripting`**.

### Values Dictionary

Tag1DataType = 3

Tag2DataType = 4

### Expressions

`Tag 1 is of Type {Tag1DataType:enum:ETS.Core.Enums.DataType}`

`Tag 2 is of Type {Tag2DataType:enum:ETS.Core.Enums.DataType}`

### Results

Tag 1 is of Type Double

Tag 2 is of Type Boolean

## Custom Enums

For enums that are defined in TrakSYS script classes (like the Developer | Scripts | Web or Global user interfaces), the assembly name must be included in the expression syntax (see examples below). The assembly name for TrakSYS script is `Ts.Scripting`.

Assuming an enum is defined in Web scripts...

```csharp
namespace MyCustomNamespace
{
    public enum MyCustomEnumType
    {
        ValueOne = 1,
        ValueTwo = 2
    }
}
```

### Values Dictionary

CustomEnumValue1 = 1

CustomEnumValue2 = 2

### Expressions

`Custom Enum 1 is {CustomEnumValue1:enum:MyCustomNamespace.MyCustomEnumType, Ts.Scripting}`

`Custom Enum 2 is {CustomEnumValue2:enum:MyCustomNamespace.MyCustomEnumType, Ts.Scripting}`

### Results

Custom Enum 1 is ValueOne

Custom Enum 2 is ValueTwo

## Custom Enum Resource Translations

But that's not all! If you order now, we will throw in the ability to auto-lookup custom enum resource translations, for free!!! By defining **Resource Groups** and **Resource Items** with certain naming conventions in the **Translations** hub under **Configuration**, the expressions will automatically seek and display the proper translation based on the user's locale.

A **Resource Group** should be defined with a **Key** of "Enum" (Name can be anything). Beneath that, **Resource Items** would be defined with **Names** of the enum string designations as follows...

| Name                       | Translation     |
| -------------------------- | --------------- |
| MyCustomEnumType\_ValueOne | This is Value 1 |
| MyCustomEnumType\_ValueTwo | This is Value 2 |

### Values Dictionary

CustomEnumValue1 = 1

CustomEnumValue2 = 2

### Expressions

`Custom Enum 1 is {CustomEnumValue1:enum:ETS.Ts.Core.Scripting.MyCustomEnumType, Ts.Scripting}`

`Custom Enum 2 is {CustomEnumValue2:enum:ETS.Ts.Core.Scripting.MyCustomEnumType, Ts.Scripting}`

### Results

Custom Enum 1 is This is Value 1

Custom Enum 2 is This is Value 2
