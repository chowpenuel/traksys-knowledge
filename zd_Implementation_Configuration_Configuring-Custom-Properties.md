# Configuring Custom Properties

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360006058054-Configuring-Custom-Properties*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

Custom Properties can be used to define additional attributes for informational purposes and use in writing custom reports. Custom Properties can also be accessed by the Logic Service during scans and used as capture values or in Event Definition and KPI Calculation evaluation. 

When creating Custom Properties, a Custom Property Scheme and a Custom Property Group must also be defined. The Custom Property Schemes define sets of Custom Properties and control which entities will be assigned to the Properties. The Custom Property Groups provide an extra level of organization that can be used when creating multiple Custom Properties.

Once Custom Properties have been created, Custom Property Views can be generated for use within TrakSYS. Please note that every time Custom Property Schemes, Groups, and Properties are modified within the Configuration section, the views must be regenerated to include the changes. This article explains the standard procedure for creating and using Custom Properties.

### **Creating Custom Properties**

The following example shows how to create Custom Properties for Systems. Please note that the process shown can also be used to create Custom Properties for other entities within TrakSYS.

  1. Open the TrakSYS Web and navigate to **Configuration | Custom Properties**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737736098067)  
  

  2. Click the New button under the Schemes section to create a Custom Property Scheme.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737738717843)  
  

  3. On the resulting page, type a Name, Key, and Tab Name. Then, click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737774777363)  
  

  4. The Custom Property Scheme should now appear under the Schemes section in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737805986067)  
  

  5. Select the Newly created Custom Property Scheme and click the New button under the Groups section on the second slice to create a Custom Property Group.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737819564563)  
  

  6. On the resulting page, type a Name for the Group, then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737817811219)  
  

  7. The Custom Property Group should now appear under the Groups section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737860216083)  
  

  8. Select the newly created Custom Property Group and click the Custom Properties button under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737862511507)  
  

  9. On the resulting page, click the New button under the Custom Properties section on the second slice to create a Custom Property.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737889027987)  
  

  10. Type a Name and Key for the Custom Property. Then, select the desired Data Type and enter a Default Value if needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737922261779)  
  

  11. Click Save to apply the changes.
  12. The newly created Custom Property should now appear under the Custom Properties section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737917699219)  
  

  13. To create additional Custom Properties, repeat steps 9 through 11 as needed.
  14. Once the Custom Properties have been added, navigate back to **Configuration | Custom Properties**.
  15. Select the configured Custom Property Scheme on the first slice, then click the Entities button under the Related section on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737943251475)  
  

  16. On the resulting page, click the Assign button under the Entities section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18737964666131)  
  

  17. Choose the Systems option within the Assign Entity drop down, then click Assign.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738028162195)  
  

  18. The Systems entity should now appear under the Entities section under the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738054597267)  
  

  19. To assign additional entities, repeat steps 16 and 17 as needed.
  20. Restart the Logic Service.
  21. To view the new Custom Property options for a System, navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738072797971)  
  

  22. Select a configured Area and System on the first and second slices, then click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738078122259)  
  

  23. The new Custom Properties tab should now appear in the properties of the System. The tab will display the value defined in the Tab Name field of the Custom Property Scheme.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738124096147)  
  

  24. Clicking the tab will reveal the Groups and individual Custom Properties defined within the Custom Property Scheme.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738204142867)  
  




These values can now be modified and referenced in different areas of TrakSYS as needed. Additional information on referencing Custom Properties within different areas of TrakSYS can be found in the TrakSYS Reference Documentation section of the support site **[here](https://docs.parsec-corp.com/tsweb/custom-properties)**.

### **Regenerating Custom Property Views**

Once all changes have been made to the Custom Properties, Custom Property Views can now be generated in the TrakSYS database. Please note that the Custom Property Views will need to be regenerated every time there is a change to Custom Property Schemes, Groups, and Properties. Therefore, it is recommended to generate the Views only after all changes have been made.

  1. Navigate to **Configuration | Custom Properties**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738224751123)  
  

  2. Click the Generate Views button under the Schemes section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738227962259)  
  

  3. Click the Generate button on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738274691987)  
  

  4. The new Custom Property Views should now appear under the Views folder of the TrakSYS database.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18738269466899)


