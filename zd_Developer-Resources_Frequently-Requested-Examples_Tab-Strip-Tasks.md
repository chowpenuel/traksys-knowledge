# Tab Strip Tasks

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14643066449555-Tab-Strip-Tasks*
*Last updated: 2024-07-24T18:58:59Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

These pages show an example of using the Tab Strip Content Part in conjunction with the Task Items Content Part. It includes 2 examples:

  * Assigned Tabs - This requires specific assignment of Tab Strip values to match with a specific Task Form Item Groups. This is useful in understanding the process of the mapping, and what information is already available through the standard Task Items Content Part.
  * Scripted Tabs - This example works for any Task Definition, using Script to create and assign the tabs in the Tab Strip Content Part. This example is more complicated and builds on the logic provided in the Assigned Tabs example.



### **Page Deployment**

The following represents the intended deployment pattern of the attached Page Definitions. It represents the Hierarchy by using a Bulleted List and the Keys from the Page Definition files.

  * Tab Strip Tasks 
    * Assigned Tabs
    * Scripted Tabs



These pages can be deployed in any implementation for testing purposes, but expect to be deployed in the Demonstration Database. Both examples expect to find a Task Definition with the ID 396 for rendering purposes and may error if a Task Definition with that ID is not found. This can be adjusted in the ContentPage_Init method of the page's script to work with any Task Definition ID.

#### **Revisions**

7th March 2023 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
