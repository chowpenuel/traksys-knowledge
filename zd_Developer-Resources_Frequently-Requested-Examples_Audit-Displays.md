# Audit Displays

*Source: https://portal.parsec-corp.com/hc/en-us/articles/8131309891219-Audit-Displays*
*Last updated: 2024-07-24T18:12:53Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

These pages show an example of retrieving and visualizing information from the tAuditHeader and tAuditDetail pages. It includes two examples:

  * Audit Anything: The ability to load a single tAuditDetail record and to display it
  * Audit Tasks: A complex auditing example that loads multiple tAuditDetail and tAuditHeader examples and renders them in a custom Table View with supporting Content Parts.



### **Page Deployment**

The following represents the intended deployment pattern of the attached Page Definitions. It represents the Hierarchy by using a Bulleted List and the Keys from the Page Definition files.

  * AuditDisplays 
    * AuditAnything
    * TaskList 
      * AuditTasks (Spoke)



#### **Revisions**

27th July 2022 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
