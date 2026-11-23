# User Slot Management Best Practices

*Source: https://portal.parsec-corp.com/hc/en-us/articles/54644061930259-User-Slot-Management-Best-Practices*
*Last updated: 2026-08-20T21:43:16Z*

---

Applies To | TrakSYS 10+

### Summary

Each TrakSYS license has a defined number of User Slots available for concurrent users accessing the TrakSYS Web. If this limit is reached, an "Exceeded amount of Concurrent Users" error message will appear for each user that attempts to access the TrakSYS Web. An example of this error message is shown below:

![](https://portal.parsec-corp.com/hc/article_attachments/54644102117395)

This article provides recommendations and best practices for managing User Slots and helping to prevent the Concurrent Users error message from appearing.

### User Tracking Behavior

As part of the User Slot tracking behavior, TrakSYS uses cookies to help identify a specific device and browser combination. When a user first accesses the TrakSYS Web with a specific device and browser, the cookie is created and a User Slot is consumed. While the user has browser windows open that are actively viewing the TrakSYS Web, the slot will be maintained for that user and will count towards the User Slot limit. Once a user closes all browser windows accessing the TrakSYS Web on a device, a countdown to free up the user will commence. If the user does not access the TrakSYS Web with the same device and browser combination for 10 minutes, then the User Slot will be freed up and a different device and browser combination can use the User Slot. However, if that user does access the TrakSYS Web within the 10 minute window with the same device and browser combination, the countdown will be cancelled and the User Slot will be maintained.

Note that a User Slot for a typical user is tracked by a unique device and browser combination. It is **not** tracked by specific user accounts. This means that once a unique device and browser combination is used, multiple users can log in and out with that combination and only consume a single User Slot. This applies to all types of users (TrakSYS, Windows, SAML, OIDC, and EVERYONE).

This behavior is slightly different if the user account is marked as a [Reserved User](https://portal.parsec-corp.com/hc/en-us/articles/360007777053-Reserving-a-User-in-the-TrakSYS-Web). When a Reserved User logs into the TrakSYS Web, the unique device and browser combination will now have a 7 day (i.e., 1 week) lock on the User Slot. Similar to normal users, if a Reserved User closes all browser windows accessing the TrakSYS Web, a countdown will commence and will be freed up in 7 days. If the user accesses the TrakSYS Web within that period of time, the countdown will be cancelled and reset the next time all browser windows are closed.

### Recommendations

The following recommendations can be used to help efficiently manage User Slots and to ensure they are available when needed:

  * When viewing the TrakSYS Web, use the same type of browser for all windows on a device at the same time. For example, don’t access the TrakSYS Web with Microsoft Edge, then open another window using Google Chrome at the same time on a device. Each type of browser takes a User Slot, as a separate cookie will be created for both browsers. If you use two types of browsers on a single device, then two User Slots will be taken for that device (one for each unique device and browser combination).  

  * Always close all browser windows accessing the TrakSYS Web on a device when a user is done accessing the web portal. Doing so will start the 10 minute countdown to free up the User Slot for the next user that may need it.  

  * When accessing pages in the TrakSYS Web, use only either the server DNS name or the server IP address in the URL. Since TrakSYS uses cookies as part of the process for identifying users, the cookies themselves are scoped to the host portion of the URL as one of the factors (http://servername/TS). If a user switches between the DNS name and the IP address, a separate cookie will be created for both types of URLs. When viewing pages or doing development work, it is recommended to only use either the DNS name or the IP address to avoid using extra User Slots.  

  * Avoid using Incognito or InPrivate browser windows. This mode usually blocks or discards cookies after a user closes a browser window or for each browser window that is opened. Therefore, a User Slot will be consumed for every Incognito/InPrivate browser window that is opened.  

  * If Reserved Users are used in production and a backup of that database needs to be restored to the development environment, temporarily remove the reservations first. If these are left as-is, the reservations will lock the User Slots for a full 7 days before they can be accessed. This can create access issues in development as the development license typically has significantly fewer User Slots than the production license.  

  * Use the built-in Active Users page (under **Administration | Diagnostics | Active Users**) to monitor the currently active User Slots. This can give a good indication of which devices access the TrakSYS Web most frequently or if multiple User Slots are being consumed by the same device.  

  * Ensure that TrakSYS can detect the computer name and IP Address of the client accessing the TrakSYS Web. If the computer name and the IP address is not accessible, the Name for the Active User Slot will display as "TIMEOUT" on the Active Users page.  

  * Ensure that cookies are not blocked or disabled at the browser level or through group policies. If cookies cannot be created, a new User Slot will be consumed every time the user navigates to a different page. If the page uses a built-in refresh mechanism (such as a Page Definition timer or a Refresh Key), a User Slot will be consumed on every page refresh.



#### For TrakSYS 11.2.2+

  * It is recommended to configure a [timeout for inactive users](https://portal.parsec-corp.com/hc/en-us/articles/4415794877715-Setting-A-Timeout-For-Inactive-Users). When a user is timed out for inactivity, they will be redirected to a special page that does not consume a User Slot. Additionally, when a user timeout occurs, the User Slot is immediately freed up instead of having to wait for the 10 minute timer.  

  * Users with the proper permissions can [kick active users from the TrakSYS Web](https://portal.parsec-corp.com/hc/en-us/articles/4415794912019-Kicking-Active-Users-In-The-TrakSYS-Web). Similar to the inactive timeout feature above, once a user is actively kicked, they are redirected to a special page that does not consume a User Slot. Additionally, the User Slot is immediately freed without waiting for the 10 minute timer.  

  * It is recommended to have at least one full administrative user marked as a Reserved User on a dedicated machine. This way, if all User Slots are consumed, the administrative user can navigate to the Active Users page and kick active users to free up slots.


