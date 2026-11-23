# Configuring the First Day of the Week

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15024802588563-Configuring-the-First-Day-of-the-Week*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### Summary

In TrakSYS, the default week starts on Sunday and goes through Saturday. However, in some cases, the week should start on a different day. In situations like this, it is important as several parts and pages within the TrakSYS Web can depend on the value set for the first day of the week. This value also determines the values generated in the tCalendar table. This table is used when TrakSYS calculates the calendar and production date values in the data. This specifically is used when TrakSYS determines the current week values in the data and SQL views. This article provides the procedure for changing the first day of the week and regenerating the entries in the tCalendar table.

### Procedure

  1. Open the TrakSYS Installation Manager and navigate to the Overview tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41184280594579)  
  

  2. Click the TrakSYS Settings button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15060886784915)  
  

  3. Scroll down to the General section. At the bottom of this section, the WeekStartDay setting is available. The default value for this field is Sunday.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15060985331219)  
  

  4. Select a new day from the drop down. The value will now appear in bold, indicating that a new value has been selected. For this example, Monday was chosen as the first day of the week.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15061049833363)  
  

  5. Click OK to apply this change. This will immediately start the update process on the tCalendar table. This process regenerates the records in this table to account for the change in the WeekStartDay.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15061088533011)  
  

  6. Once the process successfully finishes, click the Done button.


