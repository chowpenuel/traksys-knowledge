# User

## IUserInfo User

The `UserInfo` class contains information about the currently logged in User.

### Properties

```csharp
string AuthenticationType
```

Returns the Authentication Type of the User (e.g. Windows, TrakSYS, etc.).

```csharp
string DisplayName
```

Returns the Display Name of the User.

```csharp
IReadOnlyList<string> EtsGroups
```

Returns a list of the TrakSYS Groups the User belongs to.

```csharp
bool IsAnonymous
```

Returns whether or not the User is an Anonymous User.

```csharp
string Locale
```

Returns the Locale of the User as per their Configuration.

```csharp
string Login
```

Returns the Login of the User.

```csharp
int UserID
```

Returns the unique identifier of the User from the TrakSYS database.

```csharp
IReadOnlyList<string> WindowsGroups
```

Returns a list of Windows Groups that the User belongs to.

### Methods

```csharp
IReadOnlyList<DbRole> GetRolesAssigned()
```

Returns a list of Roles that have been assigned to the User.
