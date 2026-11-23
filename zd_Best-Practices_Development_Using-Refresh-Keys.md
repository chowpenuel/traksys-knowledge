# Using Refresh Keys

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115010453508-Using-Refresh-Keys*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

### Summary

Page definitions have a Refresh (Minutes) property. This is for situations where a constant, periodic refresh of the page is needed, as in previous versions. Unlike previous versions, the rate can no longer be specified in seconds on the page definition but minutes.

Starting with TrakSYS 10 there is a new page-refreshing paradigm, called Refresh Keys, that will address many if not most implementation scenarios (especially when refreshes take place at rates greater than once per minute or across many pages). With Refresh Keys, rather than having the page automatically refresh based on a timer, the web server will trigger a page refresh only when there is an update to the page. In effect, the server will push any changes to the page, rather than have the page poll for updates by periodically refreshing. The fundamental reason for this new approach is that it drastically reduces server load compared to using constant refresh timers.

The use of Refresh Keys allows refreshing the page either when there are changes to certain configuration entities (systems and tags) or via an API call:
    
    
    this.Ets.Pages.BroadcastChangeNotificationForKey("myKey");  

(unless a built-in Content Page is used). In this way, needless periodic refreshes are eliminated and the page only updates when something has changed.

### Configuring a Refresh Key

  1. In the Configuration section, navigate to the entity (System or tag) for which the Refresh Key will be added and edit its properties. In this example, we will use a system:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18704844821779)  
​
  2. In the Advanced tab, enter a unique string for the Refresh Key property and click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18705140842387)​
  3. In the Developer section, edit the properties of the page definition.
  4. In the General tab, verify the Refresh (Minutes) property is set to zero then enter the same unique string from step 2 for the Refresh Keys property and click Save:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18705042089619)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18705075009171)  
​
  5. Restart Logic Service



Now, when there is a change to the system (new event, job change, product change, new KPI interval, etc), any page with the same Refresh Key will be refreshed automatically. Also, note that multiple Refresh Keys can be specified for a given page definition so the refreshing is not limited to only one system and/or tag.
