# Converting Task Definitions to Task Forms

*Source: https://portal.parsec-corp.com/hc/en-us/articles/48443813968659-Converting-Task-Definitions-to-Task-Forms*
*Last updated: 2026-05-19T17:40:46Z*

---

Applies To | 14.0.0+

### Summary

With TrakSYS 14, Task Forms were introduced as an extension to Task Definitions, enabling new functionality such as versioning and expanded trigger configuration. To leverage these features, existing configuration must be migrated from Task Definitions to the Task Form model. Although the overall configuration approach remains similar, it relies on different entities and relationships, and manually reconfiguring a large number of Task Definitions can require significant effort.

To facilitate this transition, a simple utility page has been provided for review and testing prior to use. This solution includes a basic user interface, usage instructions, and commented code that can be further modified if needed. It is designed as a starting point for developing a more tailored conversion tool to assist implementations upgrading from earlier versions to the newer model.

Before using the utility, it is strongly recommended to review the included instructions, code comments, back up the database, and validate the behavior in a test environment.

#### See Also

  * [Configuring Task Forms](https://portal.parsec-corp.com/hc/en-us/articles/48443733495059-Configuring-Task-Forms)

  * [Using Task Form Item Conditionals](https://portal.parsec-corp.com/hc/en-us/articles/48443764434195-Using-Task-Form-Item-Conditionals)




#### Downloads
