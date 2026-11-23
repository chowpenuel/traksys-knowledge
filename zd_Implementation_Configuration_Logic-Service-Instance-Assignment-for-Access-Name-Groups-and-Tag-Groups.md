# Logic Service Instance Assignment for Access Name Groups and Tag Groups

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15877066249747-Logic-Service-Instance-Assignment-for-Access-Name-Groups-and-Tag-Groups*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12+

### **Summary**

In TrakSYS 12, the ability to assign Logic Service Instances to Access Name Groups and Tag Groups was added. This feature provides more granular control over which Logic Service will load specific Access Names and Tags. This is especially useful for Multi-Site installations and Single Site installations that have multiple Logic Services.

However, with this addition, all Access Name Groups and Tag Groups are now required to have a Logic Service Instance assigned. If no assignment is made on either of these entities, then the associated Tags and Access Names may not load when the Logic Service is started. Additionally, some Access Names and Tags may not be selectable in the appropriate pickers when configuring other related entities using the built-in configuration pages.

**Note** : If a Single Site installation is used and there is only one Logic Service Instance available, then that instance should be assigned to all configured Access Name Groups and Tag Groups. When only one Logic Service is configured, all new Access Name Groups and Tag Groups will have the existing Logic Service automatically assigned to them.

### **Logic Service Instance Assignment for Access Name Groups**

The following steps assume that one or more Access Name Groups have been configured and exist within the installation.

  1. Access the TrakSYS Web and navigate to **Configuration | Tags | Access Names**.
  2. Double click the desired Access Name Group in the first slice.
  3. On the resulting page, choose a Logic Service Instance under the Logic Service property. Then, click the Save button to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16252560191891)  
  

  4. Start (or restart) the Logic Service to apply the changes.



### **Logic Service Instance Assignment for Tag Groups**

The following steps assume that one or more Tag Groups have been configured and exist within the installation.

  1. Access the TrakSYS Web and navigate to **Configuration | Tags**.
  2. Click the desired Tag Group in the first slice. Then, click the "Set Logic Service" link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16252371758483)  
  

  3. Select a Logic Service Instance from the dropdown and click the Assign button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16252462128915)  
  

  4. Start (or restart) the Logic Service to apply the changes.


