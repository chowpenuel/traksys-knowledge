# Enabling Load All Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115004469754-Enabling-Load-All-Tags*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

Enabling the Load All Tags feature can be useful as a means to ensure that all tags are loaded when the Logic Service is started. Any tags that are not used in the configuration or are not being referenced by other tags will not be loaded when the Logic Service is started. Load All Tags will load every tag in the TrakSYS implementation, regardless of whether the tags meet this criteria. By default, this option is disabled when a new Logic Service Instance is created.

**Generally, it is not recommended to leave this option on permanently, as this may cause performance issues in TrakSYS implementations that have a large amount of tags.** If loading tags that are not part of the configuration or are not being referenced by other tags is required, it is recommended to assign these tags to the Logic Service or a System as explained **[here](https://portal.parsec-corp.com/hc/en-us/articles/115004469774-Assigning-Tags-to-Systems-and-the-Logic-Service)**.

### **Procedure**

  1. Open the TrakSYS Installation Manager and stop the Logic Service.
  2. Open the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18767066282643)  
  

  3. Select the configured Logic Service Instance on the second slice and click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18767123802771)  
  

  4. On the resulting page, navigate to the Advanced section and check the Load All Tags checkbox.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18767178034067)  
  

  5. Click the Save button to apply the changes.
  6. Go back to the TrakSYS Installation Manager and start the Logic Service.



To disable the Load All Tags option, repeat the steps listed above and uncheck the Load All Tags checkbox. Then, click Save to apply the changes.
