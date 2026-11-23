# Displaying Images from an External Source

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14459281976595-Displaying-Images-from-an-External-Source*
*Last updated: 2024-07-24T18:40:15Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

This page show an example displaying an image in the TrakSYS Web using a file found on the host server. 

### **Page Deployment**

There is only one page included in this example (PageDefinition_ExternalImageDisplay.pdef). However, it does require an image file to be provided. An image has been included (parsec-logo-blue.png), but any image can be used, as long as the page's script is updated to reflect the new file. The image file is expected to be placed in the TrakSYS program files under the following relative path:
    
    
    ~TrakSYS\ts\WebImages\parsec-logo-blue.png

The example uses a folder called "WebImages" that will need to be created. The folder **is not necessary** for the functionality to work, but is generally recommended. Alternatively, a different file path can be used, but the page script will need to be updated accordingly. See the page's script and the provided comments for more details.

#### **Revisions**

1st March 2023 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
