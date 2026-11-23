# Alternate Content Parts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/39578891445523-Alternate-Content-Parts*
*Last updated: 2025-10-17T17:45:35Z*

---

### **Introduction**

This article provides Content files for a Frequently Requested Example (FRE). The Content provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to supplement the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Content files. The intended way to implement this Content as well as a short description of the capability they are meant to provide is listed below. 

### **Capability**

These content files are custom Content Parts that mirror the functionality of existing TrakSYS Content Parts, with minor modifications. The package includes two examples:

  * **Extended Keystroke Listener** – Overrides two of the standard values for the Keystroke Listener part.

  * **Extended Menu** – Adds default values to the `MenuInfo` list, which is blank in the standard Menu part.

  * **Extended Table View Interactive -** Adds default values to the ColumnInfo list, which is blank in the standard Table View Interactive part.




This is achieved by creating new Content Parts that **inherit** from the standard `ContentPart` and modifying the base constructor. While specific changes will vary, the general pattern shown here can be applied to any existing Content Part.

This functionality can also be used alongside other Content Part features, such as adding new Content Property Attributes and implementing additional data processing.

### **Content Deployment**

The Content can be imported into any site through the Developer sections by doing the following:

  1. Navigate to the Developer section of any site.

  2. Select the Content Hub.

  3. Select the Parts Hub.

  4. Under the Groups header, select Import.

  5. Use the file explorer to locate and select the `.content` file.

  6. Repeat this step for any additional `.content` files.




The imported content will appear under its original grouping. If the expected group does not exist, it will be created automatically. These parts are configured in a group named **"** FRE Examples**."**

#### **Revisions**

17th October 2025 - Added Extended Table View Interactive example (v12.0.4)

27th March 2025 - Initial Publication (v12.0.3) [includes older part and group names]

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
