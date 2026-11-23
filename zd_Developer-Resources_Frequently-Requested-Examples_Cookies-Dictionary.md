# Cookies Dictionary

*Source: https://portal.parsec-corp.com/hc/en-us/articles/8133044912275-Cookies-Dictionary*
*Last updated: 2024-07-24T18:19:57Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

These pages show an example of using the Cookies Dictionary. This functionality was introduced to replace the Sessions Dictionary for various technical reasons. This example features rebuilt versions of the Oee, Availability, Performance, and Quality Content Pages, each modified with minor scripting and parts to use the Cookies Dictionary. When a Filter is used on one of the pages, it will be saved to the Cookies Dictionary. When one of the pages loads, it will check the Cookies Dictionary to see if a value has already been set.

There are more nuances to the logic used, but the details can all be found in the "Cookies" page definition, as well as the script of the individual reports.

### **Page Deployment**

The following represents the intended deployment pattern of the attached Page Definitions. It represents the Hierarchy by using a Bulleted List and the Keys from the Page Definition files.

  * Cookies 
    * vOee (spoke)
    * vAvailability (spoke)
    * vPerformance (spoke)
    * vQuality (spoke)



#### **Revisions**

27th July 2022 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
