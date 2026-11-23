# Configuring Template and Child Systems

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360006058174-Configuring-Template-and-Child-Systems*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

A System Template is a specially marked System in the configuration from which Child Systems can inherit. Child Systems that inherit from a System Template receive nearly all of the parent’s configuration settings, Sub-Entities (Event/Function/Task Definitions, KPI Calculations, etc), and their settings.

Properties that must be System specific (e.g. Product Sets and Schedules) are unlocked at the inheriting System level on the Child System for individual configuration. Changes made at the System Template are propagated to all of the associate children. In turn, deleted entities under the System Template are also removed from the inheriting Systems.

Template Systems are useful for quickly creating multiple Systems with similar settings and entities. Most customizations cannot be made on an individual Child System. If the System needs to deviate from the Template, it may be detached from the Template. However, once a Child System is detached, it cannot be reattached. This article explains the standard procedure for creating and configuring Template Systems.

### **Creating a Template System**

This section will show how to create a Template Discrete System. Please note that this same procedure can be used to create Template Batch and Storage Systems.

  1. Open the TrakSYS Web and navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735780814227)  
  

  2. Select a configured Area on the first slice. Then click the New button on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735754509331)  
  

  3. On the resulting page, click the Template Discrete System option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735801653139)  
  

  4. Type a Name for the Template System. Then navigate to the Advanced tab and set a Template Tag Prefix. This property is used when assigning Tags to Child Systems. The Template System and all Child Systems must have a set Template Tag Prefix.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735847609107)  
  

  5. Continue configuring the Template System as needed. Please note that most configurations that are made on this System will also be transferred to Child Systems created under it. Once all of the desired changes have been made, click the Save button.
  6. To create a Child System, select the newly created Template System under the Systems section and click Create Template Child System under the Actions section on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735852778899)  
  

  7. Click the Create button on the resulting page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735901776787)  
  

  8. Select the newly created Child System and click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18735958023443)  
  

  9. Navigate to the Advanced tab within the Discrete System Properties. In the Name field, rename the Child System. Then, give the System a Template Tag Prefix.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736012986771)  
  

  10. Continue configuring the Child System as needed. Please note that only certain System-specific properties (e.g. Schedule, Location, and Product Set) can be modified at the inheriting System level. Options that are disabled on the Child System can only be changed at the System Template.
  11. Once the desired changes have been made, click the Save button.
  12. The Template and Child Systems should now be displayed under the Systems section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736075422483)  
  

  13. Additional Child Systems can be created by repeating steps 6 through 11 shown above.



### **Creating a Template System from an Existing System**

In TrakSYS 10, the ability to create a Template System from an existing Discrete, Batching, or Storage System was added. Once a template is created from the original System, that System is automatically converted into a Child System of the Template. **Please note:** a configured Tag Group for the Template must be present before creating the new Template System.

  1. Open the TrakSYS Web and Navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736072062483)  
  

  2. Select a configured Area on the first slice, then select a configured System on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736142989203)  
  

  3. On the third slice, click the Create Template Parent System button under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736139624467)  
  

  4. On the resulting page, enter a Parent Template Tag Prefix and the Tag Group ID of the Tag Group that will be used for the Template System. Then click the Create button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736206746515)  
  

  5. The new Template System should now be present under the Systems section and the existing System should now display as a Template Child.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736254489363)  
  

  6. The Template System can then be configured as needed.



### **Detaching a Child System from a Template**

A Child System can be detached from a Template System if it needs to deviate from the settings configured in the Template. **Please note that once a Child System has been detached from the template, it cannot be reattached in the future.**

  1. Open the TrakSYS Web and Navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736339758099)  
  

  2. Select a configured Area on the first slice, then select a Child System on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736448904595)  
  

  3. Select the Detach From Template Parent button under the Actions section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736464580755)  
  

  4. On the resulting page, click the Detach button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736497883411)  
  

  5. The System will now be considered a normal System and will not display "Template Child" in the description.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18736506221971)



#### **See Also**

  * [Creating and Assigning Tags to Template and Child Systems](https://portal.parsec-corp.com/hc/en-us/articles/360007284233-Creating-and-Assigning-Tags-to-Template-and-Child-Systems)


