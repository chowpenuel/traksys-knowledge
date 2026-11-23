# Why is the scheduled night shift showing on the previous day instead of the current day?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15025428533907-Why-is-the-scheduled-night-shift-showing-on-the-previous-day-instead-of-the-current-day*
*Last updated: 2025-05-21T21:58:47Z*

---

Applies To | TrakSYS 10+

If a scheduled night shift goes through midnight and the Schedule Pattern Item has the Shift Date set to “Based on Start Date,” then the night shift will show as a shift from the previous day. in order to include the night shift on the current day, the Shift Date will have to be set to “Based on End Date.” 

**Note:** This setting is irrelevant to shifts that start and end on the same day. These shifts will always appear on the day that they were scheduled.

The following steps describe how to change the Shift Date setting:

  1. Stop the Logic Service.
  2. Access the TrakSYS Web and navigate to **Configuration | Schedules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542136422931)  
  

  3. Select the desired Schedule Group within the first slice. Then, select the desired Schedule in the second slice.
  4. On the third slice, click the Edit button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542183507859)  
  

  5. Check the "Allow Schedule Edits (Edit Mode)" setting, then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542288765075)  
  

  6. Next, click the Schedule Patterns link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542264145043)  
  

  7. Click the desired Schedule Pattern on the second slice.
  8. On the third slice, click the Calendar link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542297536147)  
  

  9. Click a Schedule Pattern Item that spans through midnight on the Calendar View. On the third slice, click the Edit button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542333618067)  
  

  10. Change the Shift Date property to "Based on End Date" and click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18542369849875)  
  

  11. Repeat steps 9 and 10 for each Schedule Pattern that runs through midnight. Once all changes have been made, click the Close button in the Schedule Pattern View.
  12. Finally, take the schedule out of Edit Mode by unchecking Allow Schedule Edits (Edit Mode). This can be accomplished by repeating steps 2 through 5.   
**Note:** The Logic Service will not start if the Schedule is left in Edit Mode.
  13. Start the Logic Service to apply the changes to the configuration.


