# Tracking User Login and Logout Activity

*Source: https://portal.parsec-corp.com/hc/en-us/articles/39371829601555-Tracking-User-Login-and-Logout-Activity*
*Last updated: 2025-07-09T22:31:22Z*

---

Applies To | TrakSYS 13.0.0+

### Summary

With the release of TrakSYS 13, a significant enhancement has been introduced to improve user session traceability and system auditing: the tUserLog table. This new feature provides a more robust and centralized approach to logging user authentication events such as logins, logouts, and failed login attempts across various user types.

The tUserLog table was introduced in TrakSYS 13 to centrally and consistently record user session activity. It captures key authentication events (such as logins and logouts) and replaces the deprecated tAuditUserActivity table. This update enhances visibility into user access patterns and supports more effective auditing and monitoring across the system.

The tUserLog feature in TrakSYS 13 requires no configuration or setup. It is automatically enabled by default and cannot be disabled. This ensures consistent logging of user session activity across all environments.

**Note** : There is no user interface (UI) for configuring this feature, and there is no API model available for accessing the data programmatically.

#### tUserLog Table Structure and Field Details

The tUserLog table in TrakSYS 13 contains the following fields to track user session activity:

  * Login: The username of the user attempting access.
  * LogDateTime: The timestamp when the login, logout, or session timeout occurred.
  * UserID: The internal identifier of the user. This corresponds to the UserID in the tUser table.
  * UserType: Indicates the type of user (link to UserType enum)
  * UserAction: Describes the type of event, such as login, logout, or failed login. (linked to UserAction enum)
  * IPAddress: The IP address from which the user attempted access.
  * ClientAgent: Information about the client software or browser used to access the system (e.g., Chrome, Edge, etc.).



### Enums

#### Enum: UserType

  * 1 – WindowsUser
  * 2 – WindowsGroup
  * 3 – TrakSYS User
  * 4 – TrakSYS Group
  * 8 – Everyone
  * 9 – OidcUser
  * 10 – OidcGroup
  * 12 – SamlUser
  * 13 – SamlGroup



#### Enum: UserAction

The UserAction field captures the result or outcome of a login attempt. The known values are:

  * 0 – Error
  * 1 – Login
  * 2 – Logout
  * 3 – LoginFailed
  * 4 – LogoutKicked
  * 5 – LogoutInactive


