# Using the TrakSYS Historian

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360005775213-Using-the-TrakSYS-Historian*
*Last updated: 2025-05-21T22:09:36Z*

---

Applies To | TrakSYS 10+

### Summary

In order to use the Historian feature within TrakSYS, a separate Historian Database must be created to store the Historian data. The database can be created using the TrakSYS Installation Manager. Also, a Historian Service Instance must be created and configured in order to start and run the Historian Service.

Once the database and Historian Service Instance has been created, Tag History Definitions must be configured for individual Tags. A Tag History Definition defines the criteria and time intervals for recording Tag values by TrakSYS for historical analysis and reporting. Multiple Tag History Definitions can be created for a Tag in order to support different visualizations and reporting requirements of the data. In order to use Tag History Definitions, the Historian feature line must be present on the TrakSYS license.

Once Tag History Definitions have been configured, the Historian Service can then be started. Tag values can then be recorded in the appropriate tables within the Historian Database. This article explains the standard procedure for setting up and using the Historian feature within TrakSYS 10 and newer.

### Creating a Historian Database

A Historian Database must be created before the Historian feature can be used within TrakSYS. In order to create the database using the TrakSYS Installation Manager, do the following:

  1. Open the TrakSYS Installation Manager and navigate to the Database section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41183546123027)  
  

  2. If no Historian Database is present, a "Database Not Found" message should appear under the Historian Connection Status section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554091323539)  
  

  3. Click the Create Historian button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360007321514)  
  

  4. Enter the connection information, then click OK.
  5. To use the default options shown on the resulting dialog, click OK. Otherwise, make any adjustments to the appropriate fields, then click OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554160337043)  
  

  6. Once the process succeeds, the Historian Connection Status should display a "connected" status.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554106339347)



### Creating and Configuring a Historian Service Instance

A Historian Service Instance must be created so the service can start and run. This service collects values from Tags that have configured Tag History Definitions (shown in the next section of the article) and pushes them to the appropriate tables within the Historian Database. In order to create a Historian Service Instance, do the following:

  1. Open the TrakSYS Web (typically http://<ServerName>/ts).
  2. Navigate to **Configuration | Services | Historian Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554139415571)  
  

  3. On the first slice, click the New button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554180077971)  
  

  4. Enter a Name for the Service Instance and the Computer Name of the server where the Historian Service is installed (typically the same server as TrakSYS). Please note that the Computer Name must be correct or the Historian Service will not start. Also note that only the name of the machine is needed in the Computer Name field. It is not necessary to enter the fully qualified domain name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554244485651)  
  

  5. Click Save to apply the changes.
  6. The Configured Historian Service Instance should now appear under the Historian Services section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554233857811)



### Creating and Configuring Tag History Definitions

Tag History Definitions can be created to determine which Tag values are recorded in the Historian Database, along with the interval in which they are recorded. Please note that the Historian Service will not run until a Tag History Definition is created and configured. In order to configure a Tag History Definition, do the following:

  1. Open the TrakSYS Web (typically http://<ServerName>/ts).
  2. Navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554233069843)  
  

  3. Select the desired Tag Group on the first slice, then select a Tag on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554286605331)  
  

  4. On the third slice, click the Tag History Definitions button under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554282268691)  
  

  5. Click the New button on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554343504019)  
  

  6. Within the Properties of the Tag History Definition, enter a Name, select a Mode, and ensure that a configured Historian Service is selected. Additional options can also be set to further control how and when Tag values are recorded. More information about these options can be found in the [TrakSYS 11 Reference Documentation](https://support.parsec-corp.com/refdocs/11/traksys/entity-reference/configuration-entities/tag-history-definition.html).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554415872659)  
  

  7. Click Save to apply the changes.
  8. The newly created Tag History Definition should now appear on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18554448000531)  
  

  9. Repeat this process to create additional Tag History Definitions as needed. 
  10. Restart the Logic Service to apply the configuration changes.
  11. Start the Historian Service to begin recording Tag values.



### Matching Historian Data to Tag History Definitions

When tag values are recorded, each Tag History Definition will have its own table within the Historian Database. However, the table for a Tag History Definition will not be created until a Tag value has been recorded by the Historian Service. Each table can be matched to its corresponding Tag History Definition by looking at the value contained within the name of the table. This value represents the ID of the Tag History Definition.

For example, using the Historian Database created in the example shown above, Tag values were recorded and stored within the table created for the Tag History Definition. 

![](https://portal.parsec-corp.com/hc/article_attachments/18554460038163)

The value of 1 shown at the end of the table name is referencing the Tag History Definition with an ID of 1. If the configured History Definition is viewed within the TrakSYS Web, the ID can be verified when it is selected and the properties are displayed on the third slice of the page.

![](https://portal.parsec-corp.com/hc/article_attachments/18554530834579)

Alternatively, the History Definition can be queried from the tTagHistoryDefinition table using the Tag History Definition ID.

![](https://portal.parsec-corp.com/hc/article_attachments/18554568155411)
