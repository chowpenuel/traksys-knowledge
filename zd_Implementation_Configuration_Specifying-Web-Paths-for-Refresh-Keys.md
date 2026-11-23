# Specifying Web Paths for Refresh Keys

*Source: https://portal.parsec-corp.com/hc/en-us/articles/47613873425299-Specifying-Web-Paths-for-Refresh-Keys*
*Last updated: 2026-03-03T01:10:56Z*

---

### Summary

When installing the TrakSYS Web, there are scenarios where changes need to be made to Internet Information Services (IIS) and to the URL used to access the Web. This can include changes such as enabling HTTPS within the web, configuring redirects to different URLs, and more. When doing so, it is necessary to provide the new URL values in TrakSYS so that Refresh Key broadcasts are correctly routed to the new links. This article contains the steps for providing the correct URLs and ensuring that Refresh Key broadcasts are correctly routed.

### Procedure

  1. Access the TrakSYS Installation Manager and navigate to the Overview tab. Then, click the TrakSYS Settings button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47614494792851)  

  2. Locate the WebServerPaths setting under the Webs section near the bottom of the Settings dialog. Then, click the ellipsis to open the String Collection Editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47614469634963)  

  3. Within the editor, enter the URL that is used to access the TrakSYS Web. In general, the URL should use the following format:
         
         http://ServerName/ts

  
If HTTPS is enabled, then the secure URL link should be used instead. An example of this is shown below:
         
         https://ServerName/ts

  
**Note** : When using HTTPS, the URL **must** match the Web URL provided on the certificate within IIS. If there is a mismatch between the URL specified in this property and the URL on the certificate, Refresh Key broadcasts will not reach their intended targets. The URL format is implementation specific, but can typically follow the format below:
         
         https://ServerName.DomainName.com/ts

  
![](https://portal.parsec-corp.com/hc/article_attachments/47616890140435)  
  
If multiple TrakSYS Webs are configured or multiple Web Servers are available, it is possible to specify multiple URLs. This is possible by providing each URL on its own line. This is typically more common in scenarios where High Availability is configured at the Web level or multiple Web Servers are used for performance purposes. An example of this URL configuration is shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/47616865553427)  


  4. Click OK to save the changes. Then, click OK on the TrakSYS Settings dialog window to close it.



After saving all changes, it is recommended to [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application). Additionally, if there is any custom scripting within any of the TrakSYS Services that read or broadcast to Refresh Keys, these services should be restarted as well. For example, if there are Logic Service Script Classes, Module Script Steps, and Workflow Process Definition Steps that interact with Refresh Keys, then the Logic Service, Data Management Service, and Workflow Service should be restarted to load the new configuration.
