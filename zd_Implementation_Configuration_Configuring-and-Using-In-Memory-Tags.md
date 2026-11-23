# Configuring and Using In Memory Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16116838526867-Configuring-and-Using-In-Memory-Tags*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12+

### Summary

In TrakSYS 12, a new tag type called In Memory Tags was introduced. When these tags are loaded by the Logic Service, the values exist in the memory of the service. This is different from most other tag types that rely on the `tTag` table for value storage and changes. This in memory value can only be modified from within the Logic Service (e.g. Logic Service Script Classes, Script Tags, etc.). Therefore, In Memory Tags are useful for keeping track of tag values that should only be changed by custom code within the Logic Service. This helps prevent tag value changes from other areas of the application such as pages from the TrakSYS Web or direct tag value edits in the `tTag.Value` field.

Since the tag's value is stored in memory, the value is temporary and will only be retained while the Logic Service is running. Once the service is stopped or restarted, the value is lost and will be reset when the service is started up again.

### Configuring In Memory Tags

The following steps show the standard procedure for adding and configuring In Memory Tags. These steps assume that one or more Tag Groups have been configured.

  1. In the TrakSYS Web, navigate to **Configuration | Tags**.
  2. In the first slice, select the desired Tag Group. Then, click the New button on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16381901630355)  
  

  3. Select the In Memory Tag option within the New Tag list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16381959697555)  
  

  4. Within the Tag configuration, enter a Name, specify a Data Type, and click Save to store the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16386557242515)  
  

  5. The new Tag entry should now appear within the second slice of the Tags configuration page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16386609144083)



Repeat steps 2 through 4 to add additional In Memory Tags as needed. **Note** : since adding and configuring tags is considered a configuration change, the Logic Service will have to be restarted to apply the changes.

### Reading and Writing In Memory Values

As mentioned in the Summary section of this article, it is only possible to perform read and write operations to the In Memory value using the Logic Service. This means that it is not directly accessible to other areas of the application (e.g., the TrakSYS Web, Data Management Service, and Workflow).

Although In Memory Tags have an entry in `tTag` and the tag value is written to the `tTag.Value` field on change, this value is unreliable and should **not** be referenced. The database value can be modified by other areas of the application, however, changes to this field does not affect the actual in memory value. Therefore, this can affect the accuracy of the tag value if the database value is being referenced instead of the in memory value.

When directly writing values to the In Memory Tag, the `QueueTagNameEqualsForAssignment()` method should be used either within a Logic Service Script Class or within a Script Tag. The method will queue the tag value change on the Logic Service scan and update the in memory value.

When directly reading values from the In Memory Tag, the built-in Tags dictionary can be used. Like the In Memory Tag value, this dictionary is only available within the Logic Service. The dictionary has four properties that can retrieve the in memory value depending on the data type. Examples of all four properties are listed below:
    
    
    Tags["TagNameHere"].ValueInteger
    Tags["TagNameHere"].ValueDouble
    Tags["TagNameHere"].ValueBoolean
    Tags["TagNameHere"].ValueString
    

The example below combines these concepts to show how they can be implemented. This example assumes that the steps outlined in the previous section have been performed.

  1. In the TrakSYS Web, navigate to **Developer | Scripts | Logic**.
  2. Select the desired Logic Script Group on the first slice and click the New button on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16386710330515)  
  

  3. Select the Logic Service Script Class option within the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16386731970195)  
  

  4. Provide a Name for the script and click Save. For the purpose of this example, "InMemoryScript" is being used.
  5. Within the code of the Script Class, the following script is used to read and write the In Memory Tag value. On each scan, the In Memory value is retrieved, incremented by 1, and written back to memory.  
  

         
         public override void PostScan(IPostScanContext context)
         {
           //Load the tag object
           var tagObject = context.Tags["InMemoryTag"];
           //Get the current value and increment it by 1
           var newValue = tagObject.LastValueInteger + 1;
           //Write the new value to the In Memory Tag
           context.QueueTagNameEqualsForAssignment("InMemoryTag", newValue);
         }
         

  6. After saving the changes, navigate to **Configuration | Services | Logic Service**.
  7. Go into the properties of the configured Logic Service Instance and specify the Script Class Name used for the Script Class. For this example, "InMemoryScript" is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16387590402707)  
  

  8. Click Save to apply the changes. Then, start the Logic Service.
  9. In the TrakSYS Web, navigate to **Administration | Services | Logic Service**.
  10. On the Logic Service page, click the Tags button under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16387379930131)  
  

  11. On the resulting page, filter by the tag name ("InMemoryTag" in this case) and submit the results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16388572595859)  
  
The entry should appear green on the page and the value should be displayed for the tag. If the Updating option is selected on the page, the tag can be seen incrementing in real time.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16388575736083)  
  

  12. **OPTIONAL** : After the tag has been incrementing for a period of time, restart the Logic Service and view the Tags page once more. The value should reset and should be counting up starting from 0.


