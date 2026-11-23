# Device

## IDeviceInfo Device

Allows access to the `Device` class which contains properties such as `ID`, `Name`, `SystemID`, and `Values`. See the [Device](../../../../entity-reference/configuration-entities/device) topic for further details.

### Properties

```csharp
int ID
```

Returns the unique identifier of the Device from the TrakSYS database.

```csharp
string Identifier
```

Returns the identification string of the Device.

```csharp
string Name
```

Returns the name of the Device.

```csharp
int SystemID
```

Returns the unique identifier of the System associated with this Device.
