# Creating Schedule Exceptions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360017871374-Creating-Schedule-Exceptions*
*Last updated: 2025-05-21T22:09:15Z*

---

Applies To | TrakSYS 10+

### **Summary**

Schedule Exceptions provide a simple way to create temporary exceptions for the production schedule. This can be useful in situations where production is scheduled to be stopped over a period where it would otherwise be scheduled (e.g. holidays). Conversely, Schedule Exceptions can be used to schedule production time during periods that otherwise be not scheduled for production. For example, a plant has to schedule production over the weekend when normally it does not operate on weekends. Due to its correlation with Shift History records, in general it is recommended that a Schedule Exception not exceed 24 hours (e.g. if the total exception time is 48 hours then 2 24-hour Schedule Exceptions would be created). 

After a Schedule Exception is created, TrakSYS will use this exception in place of the normal Schedule Pattern for the full duration of the exception. Once the Schedule Exception has ended, TrakSYS will revert back to the Schedule Pattern with the most current Effective Date/Time for the System.

This article explains the standard procedure for creating Schedule Exceptions.

### **Procedure**

  1. Open the TrakSYS Web and navigate to **Configuration | Schedules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550075157523)  
  

  2. Select a configured Schedule Group in Slice 1, then select the desired Schedule in Slice 2.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550105570451)  
  

  3. In Slice 3, select the Schedule Exceptions link under the Related section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550125941395)  
  

  4. On the resulting page, click the New button under the Schedule Exceptions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550150923283)  
  

  5. For the Schedule Item, configure the exception as needed.  
  

     * The **Start Date/Time** and **End Date/Time** fields determine when the Schedule Exception will start and end.
     * The **Shift** and **Team** fields determine which configured Shift and Team will be assigned to the exception.
     * The **Date** field will determine the "Production Date" for the exception, analogous to the Shift History Date field. The start date value is used by default.
     * The **Scheduled** field determines whether the Schedule Exception is scheduled or not for its duration. Typically, this option should have the opposite setting of the regular Schedule Pattern Item. For example, if the normal Schedule Pattern Item has this option enabled (to indicate production normally runs for that period of time), then this option should be disabled on the Schedule Exception (to indicate that production will not be running for that length of time).  
  

![](https://portal.parsec-corp.com/hc/article_attachments/18550238559763)  
  

  6. After making the changes, click the Save button.
  7. Under the Schedule Exceptions section, a tree view should appear with the year of the Schedule Exception at the top-level.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550284512915)  
  

  8. Expanding the year should reveal the configured Schedule Exception. Notice that the entry is grayed out to indicate that the exception will contain Not-Scheduled time for the duration.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550263529619)  
  

  9. As more Schedule Exceptions are added for different years, more top level entries will appear for each year. In the example below, more Schedule Exceptions were added for years 2024 and 2025. An additional Schedule Exception was also added for 2023. Notice how the new exception is not grayed out, meaning that production is scheduled for the length of the exception.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18550371805843)


