# Reserving a User in the TrakSYS Web

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007777053-Reserving-a-User-in-the-TrakSYS-Web*
*Last updated: 2025-05-21T22:08:38Z*

---

Applies To | TrakSYS 10+

**Summary**

Reserving Users is a great way to ensure that floor terminals and other devices will have a guaranteed User slot for a longer period of time when accessing the TrakSYS Web. This helps prevent the possibility that the specific device will encounter a "Exceeded amount of Allowed Concurrent Users" error when attempting to access the TrakSYS Web.

When a User is Reserved, a slot is assigned to that device and browser combination. During the reservation period, the slot will always be assigned to it regardless of whether or not a User is utilizing it to access the TrakSYS Web. This means that the slot will not be freed up when a User is done accessing the TrakSYS Web with the device, which reduces the pool of available User slots for other potential devices. Any User that accesses the TrakSYS Web with the reserved device and browser combination may take advantage of the reserved slot.

Please note that the User must have the AllowReservedUser permission enabled in order to create the reservation. This setting can be enabled or disabled within the Role that is assigned to the User. Also, the User accessing the TrakSYS Web on the reserved device must use the browser that was utilized to create the reservation. If the User is accessing the TrakSYS Web with the same machine but with a different browser, they will not be a reserved user and the device will take up a second User slot.

Additionally, the reservation period does not last indefinitely. If a User does not access the TrakSYS Web with the device and browser combination for an extended period of time, the reservation will eventually expire. The slot can also be freed up if the reservation is manually removed for the device. Since this option can reduce the number of available slots for other devices while it's active, it's recommended to only use this open when absolutely necessary. In the majority of scenarios, enabling this option may not be necessary. 

**Procedure**

  1. Log into the TrakSYS Web with an account with sufficient privileges to reserve a user.
  2. Within the TrakSYS Web, click the user name at the top right corner of the page and click settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18546002100755)  
  

  3. In the resulting Settings page, the option to reserve a User will be under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18546050527507)  
  

  4. Once the used is Reserved, the Is Reserved User field under the User Information section should display a value of **True**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18546071736723)



To remove a Reserved User, repeat the steps above and select the **Remove Reserved User** link under the Actions section of the Settings page.

![](https://portal.parsec-corp.com/hc/article_attachments/18546085443475)

**See Also**

  * [Viewing Active and Reserved Users in the TrakSYS Web](https://portal.parsec-corp.com/hc/en-us/articles/115004920274-Viewing-Active-and-Reserved-Users-in-the-TrakSYS-Web)


