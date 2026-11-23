# Assigning Tags to Systems and Logic Service Instances

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004469774-Assigning-Tags-to-Systems-and-Logic-Service-Instances*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

If a TrakSYS installation has a large amount of Tags, it may be desirable to create a way to organize Tags by System or by Logic Service for reporting purposes. This form of organization can be achieved by assigning Tags to their respective Systems or Logic Service Instances through the use of Tag Relationships. This article explains the standard procedure for assigning Tags using Tag Relationships.

Please note that Tag Relationships are for extensibility purposes only and are not used by default. There is no data collected or stored automatically as a result of configuring System Tag Relationships.

### **Procedure**

#### **Assigning Tags to a System**

  1. Stop the Logic Service.
  2. Open the TrakSYS Web and navigate to **Configuration | Systems**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766522177683)  
  

  3. In the first slice, select a configured Area. Then, select a configured System in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766680447379)  
  

  4. Click the Tags button under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766770491923)  
  

  5. On the Tags section of the second slice, click the New button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766759814675)  
  

  6. In the name field, type a name for the Tag Relationship. Then, choose the desired tag using the tag picker button under the Relate Tag field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766834438291)  
  

  7. Once the Tag Relationship has been configured, click the Save button to save the changes.
  8. The new Tag Relationship should now appear under the Tags section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766821008275)  
  

  9. Start the Logic Service.



#### **Assigning Tags to a Logic Service Instance**

  1. Stop the Logic Service.
  2. Open the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766898396435)  
  

  3. Click the configured Logic Service on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766908292755)  
  

  4. Click the Tags button under the Related section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766922948755)  
  

  5. In the Tags section of the second slice, click the Assign button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766931949203)  
  

  6. On the resulting page, search for the desired tag. Then, click the Assign button to create the Tag Relationship.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18767012959379)  
  

  7. The Tag Relationship should now appear in the Tags section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18766965759507)  
  

  8. Start the Logic Service.


