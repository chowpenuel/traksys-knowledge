# Database Transfer Guide

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

### Summary

In many cases, making changes to a TrakSYS production server can be disruptive to real-time data collection. In an ideal scenario, configuration and user interface changes (e.g. adding a new production line) would be made in a development environment, and then pushed to the production server.

TrakSYS 10 allows users to transfer these changes from a development server to a production server using the TrakSYS Installation Manager. This article will cover best practices and procedures for executing a database transfer.

### Best Practices

#### Creating a Visual Difference Between Prod and Dev

Before transferring configuration and/or user interface changes from the development server to the production server, it is recommended to create a way to easily distinguish between the two servers. Doing so can help the user quickly determine in which environment they are working. One way to create a visual difference between the two servers is to change the background color of the navigation bar in the TrakSYS Web of the production server. For that reason, this setting is not impacted by a database transfer.

In order to change the background color of the navigation bar:

  1. Open Installation Manager.
  2. In the Overview tab, click the TrakSYS Settings option  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224306368787)  
  

  3. In the Web section of the Settings window, locate the CustomNavBarBackColor section and enter a hex value of the desired color. For the purpose of this example, the hex value for black was entered.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19222953845779)  
  

  4. Click OK to save the changes and exit.
  5. In a web browser, access the TrakSYS Web (typically **http://ServerName/ts**)
  6. Under the Administration section, click the Settings hub.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19223039939987)  
  

  7. In the Settings page, click the Reload Application button to apply the color change to the navigation bar.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19223097060243)



The navigation bar should now appear in the color that was specified in TrakSYS Settings.

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/115011009148/9308070bd336106b006053e5e0dda632ba2842fdd13fba8c6f06a8561d01bd5f.png)

#### Setting the Transfer Target

TrakSYS 10 provides a setting called IsTransferTarget that allows removing edit options for all users (including administrators) when viewing configuration settings and page definitions. Enabling this option safeguards against users inadvertently making changes on the production server. With the setting enabled, changes can only be applied via the database transfer import operation.

In order to enable the IsTransferTarget setting:

  1. Open Installation Manager.
  2. In the Overview tab, click the TrakSYS Settings option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224306368787)  
  

  3. In the General section, change the value of IsTransferTarget to True.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224381701907)  
  

  4. Click OK to save the settings and exit the window.
  5. To apply the changes, access the TrakSYS Web (typically **http://ServerName/ts**)
  6. Under the Administration section, click the Settings hub.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224452042003)  
  

  7. In the Settings page, click the Reload Application button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19223097060243)



When viewing configuration settings, options that would normally allow users to make modifications to the configuration will now be disabled.

![](https://portal.parsec-corp.com/hc/article_attachments/19224600492435)

In order to re-enable these options, change the IsTransferTarget setting back to False.

#### Excluding Fields and Tables

In certain scenarios, it may be desirable to exclude tables or fields from the transfer in order to prevent specific data on the production server from being overwritten. TrakSYS provides two settings for this purpose, called ExcludedFields and ExcludedTables.

In order to exclude tables and fields from the Transfer Export process, do the following:

  1. Open Installation Manager.
  2. In the Overview tab, click the TrakSYS Settings option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224306368787)  
  

  3. Locate the ExcludedFields and ExcludedTables settings under the Database Transfer section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224904217491)  
  

  4. To add items to the collection, click the (Collection) field, then click the ellipsis (...) to open the String Collection Editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224933288211)  
  

  5. Add the desired tables/fields to the appropriate settings, then press **OK**. Note that field names should be entered as `TableName.FieldName`.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19224980392211)



The specified tables/fields will now be excluded during the Transfer Export process.

Note that these settings can also be used to enable editing for certain parts of the configuration on the production server when IsTransferTarget is enabled. Specifying excluded tables/fields in that scenario will enable the edit options for those entities.

In the example above, tMaterial and tMaterialGroup were added as excluded tables. On a production server with IsTransferTarget enabled, the editing options for these tables would now be enabled.

![](https://portal.parsec-corp.com/hc/article_attachments/19225049696915)

### Executing a Database Transfer

#### Export

Before exporting configuration data from a development server, stop all TrakSYS services. Failure to do so may result in errors.

![](https://portal.parsec-corp.com/hc/article_attachments/41539348597651)

  1. To begin the export process, open Installation Manager and click the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41539317949459)  
  

  2. Click the Transfer Export button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19225198443027)  
  

  3. Select the desired options, then press OK.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19225230710419)  
  


**Transfer Configuration** will transfer the configuration settings (Systems, Tags, Script Classes, Products, Categories, etc.).

**Transfer User Interface** will transfer all Page Definitions along with their related Hubs and Spokes.

  4. Save the database transfer file.
  5. Copy the transfer file to the production server.



#### Import

If TrakSYS 11.1.2 or older is being used, stop all TrakSYS services before importing configuration data to the production server. The import process will not execute if there are TrakSYS services running. This does not apply to database transfers that are only transferring UI changes.

If TrakSYS 11.2.0 or newer is being used, it is possible to perform a Database Transfer while the services are running. However, this will only succeed if the changes include additions or modifications to configuration. If any entities are deleted, then the services will need to be stopped before the Import process is started. If a Database Transfer Import is initiated while the services are running, the changes will not take effect until the next service restart. This allows users to transfer configuration changes now while scheduling a service restart to apply them at a later time.

  1. In the Database tab of Installation Manager on the production server, click the Database tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41539317950355)  
  

  2. Click the Transfer Import button and select the .transfer file that was generated during the database export process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19225291485843)



Once the import process is complete, the production database will contain the transferred configuration and user interface changes.

* * *

### See Also

  * [Tables Excluded from Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115002120954)
  * [Single-Site Transfer in a Multi-Site Installation](https://portal.parsec-corp.com/hc/en-us/articles/360038561934)


