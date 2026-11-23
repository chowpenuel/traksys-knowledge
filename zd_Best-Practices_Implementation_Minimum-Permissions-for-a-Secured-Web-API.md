# Minimum Permissions for a Secured Web API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4409084922131-Minimum-Permissions-for-a-Secured-Web-API*
*Last updated: 2025-05-21T23:05:12Z*

---

Applies To | TrakSYS 11.2.0+

### Summary

Starting with TrakSYS 11.2.0, a new security option for Web API called SecuredByPermission was implemented. This option can be used along with [API Users](https://portal.parsec-corp.com/hc/en-us/articles/360058636833-Configuring-API-Users) to grant and deny specific Web API functionality based on individual users. Along with this option, a new set of TrakSYS permissions were added. These specific permissions are related to every built-in Web API call available in the TrakSYS software. The TrakSYS software does use some of these calls by default for certain functionality. Therefore, the minimum required permissions for various features are included below.

#### General Permissions

**View Tag** \- This permission is required for the [Live Tag](https://docs.parsec-corp.com/tsweb/expression-syntax/format/tag-format) functionality. When using this feature, the tag name is placed in the expression of a Content Part. When the page is viewed, the tag value is updated on the page in real time through Web API calls. Any user that is meant to view pages with this functionality should have this permission enabled.

**ViewNotificationAlert** \- This permission is required as part of the [Alert Notification](https://portal.parsec-corp.com/hc/en-us/articles/360004903154-Configuring-Notifications-and-Alerts) functionality. When an Alert is triggered TrakSYS will use Web API calls based on this permission and the bell icon will be updated for the user within the TrakSYS Web. Any users that are configured to receive Alert Notifications should have this permission enabled.

**ViewHistorian** \- This permission is required for parts of the [Historian](https://portal.parsec-corp.com/hc/en-us/articles/360005775213-Using-the-TrakSYS-Historian) functionality. This includes any of the "Live" or "Interactive" Historian Charts and Content Pages. Any users that are meant to view these parts or pages should have this permission enabled.

#### **Logic Service**

The following Web API permissions are recommended for the Logic Service at a minimum:

  * BroadcastFastUpdate
  * BroadcastRefreshKey
  * BroadcastNotificationAlert



#### **Workflow Service**

The following Web API permissions are recommended for the Workflow Service at a minimum:

  * BroadcastRefreshKey
  * BroadcastNotificationAlert



#### **Maintenance Service**

The following Web API permission is recommended for the Maintenance Service at a minimum:

  * BroadcastNotificationAlert



#### **Data Management Service**

Currently, there are no recommended permissions for the Data Management Service. This is because there is no place to store an API User Token for a Module. As such, there is no built-in functionality from this service that makes Web API calls. While doing this from a Module is possible, it does require a custom solution. Any Web API calls made by the solution will have to be maintained in the custom scripting.

#### **Historian Service**

There are no Web API permissions required for the Historian Service.
