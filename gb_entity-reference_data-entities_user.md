# User

## Summary

### Entity Name

User

### Database Table Name

`tUser`

### API Object Name

`DbUser`

### Entity Description

TrakSYS Users represent individuals that may have access to the TrakSYS user interface.

## Properties

`Type [ UserTypeID ]`

A User Type categorizing this User (solely for organizational and reporting purposes).

`Login Type [ Type ] : ETS.Core.Enums.UserType`

* **WindowsUser** = 1
* **WindowsGroup** = 2
* **EtsUser** = 3
* **EtsGroup** = 4
* **IpAddress** = 5
* **ComputerName** = 6
* **Identifier** = 7
* **Everyone** = 8
* **OidcUser** = 9
* **OidcGroup** = 10
* **ApiUser** = 11
* **SamlUser** = 12
* **SamlGroup** = 13

Specifies the type of User defined.

**Windows User** - Ties the User to an existing Windows account. The login and password for Windows Users is maintained in the Windows Active Directory.

**Windows Group** - Ties the User to an existing Windows Group definition. The Group membership Windows Groups are maintained in the Windows Active Directory.

**TrakSYS User** - Specifies that the user login and password information are to be maintained within TrakSYS.

**TrakSYS Group** - Allows individual Users to be grouped for reporting and login control purposes.

**OidcUser** – Ties the User to an existing User account from an external Identity Provider that supports OpenID Connect. The login, password and authentication are handled by the external Identity Provider.

**OidcGroup** – Ties the User to an existing Group from an external Identity Provider that supports OpenID Connect. The Group membership is maintained by the external Identity Provider.

**ApiUser** – Ties the User to a Web API request through HTTP Authorization headers. The User is maintained in TrakSYS.

**SamlUser** – Ties the User to an existing User account from an external Identity Provider that supports SAML (typically SAML 2.0). The login, password and authentication are handled by the external Identity Provider.

**SamlGroup** – Ties the User to an existing Group from an external Identity Provider that supports SAML. The Group membership is maintained by the external Identity Provider.

**Everyone** - A special type of User which will include all users attempting to access a resource. It can be used as a simple way to assign permissions to all users attempting access. It is analogous to the EVERYONE Windows Group but also includes access when the Windows User is not known or empty.

`User [ Login ]`

Specifies the Windows User name if the User is defined as a Windows User. The value specified must be unique within the User list

`Group [ Login ]`

Specifies the Windows or TrakSYS Group name if the User is defined as a Windows or TrakSYS Group. The value specified must be unique within the User list

`Login [ Login ]`

Specifies the username if the User is defined as a TrakSYS User. The value specified must be unique within the User list. Logins are not case sensitive when being entered into TrakSYS login screens.

`Password [ Password ]`

Specifies the password if the User is defined as a TrakSYS User. Passwords are case sensitive when being entered into TrakSYS login screens.

`Email Address [ Email ]`

Specifies the email address for the User. This address is used to send Notifications to the User.

`Locale [ Locale ]`

Specifies the Users preferred locale. The locale string syntax is based on standard Microsoft locale list (English US = en-us).
