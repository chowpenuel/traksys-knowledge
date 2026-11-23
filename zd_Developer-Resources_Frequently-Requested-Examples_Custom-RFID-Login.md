# Custom RFID Login

*Source: https://portal.parsec-corp.com/hc/en-us/articles/48421988709267-Custom-RFID-Login*
*Last updated: 2026-06-23T22:18:50Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

These pages show an example of a simple alternative Login page using the IClaimService. It does **not** include User Validation outside a simple External ID match and does **not** support User Types other than **ETS Users**. It is intended for use with an **RFID** card to scan an External ID and then to load the appropriate user. 

This setup may not be valid for regulated environments but can be expanded upon to build other custom Login pages. The IClaimService supports methods for login and validation of other User Types. These are **not** explored in this example.

This page was designed to help users login with an RFID reader (as this is a common use case). However, the page can be modified as needed to meet different implementation requirements instead. The page will provide a Text Box Input and the code to sign on via `tUser.ExternalID` (a good place to store an identifier value such as an RFID value, UserID, or something else). If using this field is not desirable, Custom Properties can be used as an alternative solution. However, the page will need to be modified accordingly.

Additionally, using a custom login page comes with its own caveats. One of the more noticeable ones includes the built-in Log On button. While a custom login page may be available, the default Log On option will always be available in the top corner of the navigation bar:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/48422608567315)

Currently, it is not possible to remove or modify this feature in any way. This means that at any time, a user will have the ability to completely bypass the custom login page and use the standard one instead. In this scenario, the Site will have to make it a standard procedure to use the custom login page and ignore this default login option. Enforcing this procedure may also be a concern.

Finally, when the custom login page is created the EVERYONE user will need page permissions to it (using [Roles and Page Permissions](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-Configuring-Page-Permissions-for-Roles)). This will force all anonymous users to be automatically redirected to this custom login page for authentication.

### **Page Deployment**

This FRE contains only a single page definition. It can be deployed anywhere as needed. 

#### **Revisions**

21st January 2026 - Initial Publication (v13.0.0)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
