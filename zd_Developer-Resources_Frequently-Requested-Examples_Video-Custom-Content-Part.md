# Video: Custom Content Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/45680076496531-Video-Custom-Content-Part*
*Last updated: 2025-10-16T20:48:18Z*

---

### **Introduction**

This article provides a Custom Content Part of a Frequently Requested Example (FRE). The part is intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment without review. 

Attached to this article is a file that contains the Content Part. The intended way to implement this part as well as a short description of its capability is listed below. 

### **Capability**

This part is meant to display a Video using a Library Item, Blob Item, or Source Url. It is meant to be similar to the TsImage part. It includes the following properties:

  * Autoplay
  * Show Controls
  * Loop Video
  * Mutes
  * Poster Image
  * Preload Mode
  * Height
  * Width



Some properties are hidden or commented in the associated code based upon expected use. They can be uncommented if needed.

### **Part Deployment**

There is only one part included in this example. It can imported through the standard Developer Section menus. 

### **Additional Notes**

While this part does allow for the use of Library and Blob Items as the source for rendering Videos, it is generally not recommended to store large files for extended times within the TrakSYS database. If possible, this should primarily be used with the Source URL property.
