# Why does the "An Item with the same key has already been added" error appear in Installation Manager?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/18240046886931-Why-does-the-An-Item-with-the-same-key-has-already-been-added-error-appear-in-Installation-Manager*
*Last updated: 2025-05-28T17:54:21Z*

---

Applies To | TrakSYS 10+

In some cases, it may be possible to see "An Item with the same key has already been added" when viewing the Services tab of the TrakSYS installation Manager.

![](https://portal.parsec-corp.com/hc/article_attachments/18240124032275)

This message can be caused by having multiple Service Instances with the same Host name. In a vast majority of cases, this should not be possible as the built-in configuration pages do not allow this. This indicates that custom code or raw SQL statements were used to create or modify these entries. 

To resolve this issue, the Service Instances need to be modified so they have unique Host names. It is strongly recommended to use the built-in configuration pages to do this as they provide proper error handling. To check the current Host names for the service instances, it is recommended to query the following fields in the TrakSYS database:

  * `tLogicManager.Host`
  * `tHistorianManager.Host`
  * `tModuleManager.Host`
  * `tWorkflowManager.Host`



There should be no two instances of the same type with the same Host name. For example, each `tLogicManager.Host` value should be unique. If there are any duplicates, they will need to be addressed in order to resolve the error message.
