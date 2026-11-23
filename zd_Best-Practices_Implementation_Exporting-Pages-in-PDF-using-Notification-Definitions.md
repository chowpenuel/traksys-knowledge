# Exporting Pages in PDF using Notification Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824358026259-Exporting-Pages-in-PDF-using-Notification-Definitions*
*Last updated: 2025-05-21T23:05:05Z*

---

Applies To | TrakSYS 11.1.1+

### **Summary**

In TrakSYS 11.1.1, the ability to export Page Definitions as PDF documents was added as described **[here](https://portal.parsec-corp.com/hc/en-us/articles/360051910014-Exporting-Pages-to-PDF)**. Part of this functionality includes the ability to attach any Page Definition as a PDF document to a Notification Definition. The following example assumes that a [Notification Definition](https://docs.parsec-corp.com/entity-reference/configuration-entities/notification-definition) as been configured. **Note** that the EVERYONE user in the TrakSYS Web must have access to the exported page. Attempting to export the page without this permission can create corrupt PDF documents.

### **Procedure**

  1. In the TrakSYS Web, navigate to **Configuration | Notifications**.
  2. Select the configured Notification Group in the first slice. Then, select a configured Notification Definition in the second slice.
  3. In the third slice, click the Attachments link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19228448850067)  
  

  4. On the resulting page, click the New button to create a new Notification Attachment.
  5. Provide values for the Name and File Name Content fields. Then, place the link to the desired page into the URL Content field. Ensure that the URL includes the `ts_pdf=1` query string parameter. The example below is referencing the built-in Systems configuration page. The ServerName and SiteKey variables in the URL should be replaced with the Server Name of the Application Server and Site Key respectively.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19228508154899)  
  




Once the changes are saved and the notification is sent, a PDF document of the Page Definition should be attached to the email.

![](https://portal.parsec-corp.com/hc/article_attachments/19228564300563)
