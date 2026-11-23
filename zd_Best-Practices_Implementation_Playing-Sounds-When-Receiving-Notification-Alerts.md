# Playing Sounds When Receiving Notification Alerts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/40815102049555-Playing-Sounds-When-Receiving-Notification-Alerts*
*Last updated: 2025-05-28T21:09:21Z*

---

Applies To | TrakSYS 12+

### Summary

When receiving Alert Notifications within the TrakSYS Web, it is possible to play sounds as an additional way to grab the user's attention. This is possible through the use of Library Items and JavaScript code that references built-in attributes. The following example shows how to implement this functionality globally to all pages within the TrakSYS Web.

### Procedure

This example assumes that an audio file has been downloaded and is available to use. The file used in this example is in .mp3 format, however, other audio formats (such as .wav) can also be used. Also, it assumes that one or more Alert Notification Definitions have been configured. Instructions for configuring Notification Definitions can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/360004903154-Configuring-Notifications-and-Alerts)**.

  1. Access the TrakSYS Web and navigate to **Developer | Library**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41327212874515)  
  

  2. In the first slice, select the desired Library Item Group. If no groups exist, click the New button to create a Library Item Group. For this example, a group called "Sounds" has been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41330771453587)  
  

  3. In the second slice click the New button.
  4. Within the Library Item properties, select the sound file and provide a name. The name should also include the extension of the file (which is .mp3 for this example).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41330771454867)  
  

  5. Click Save to apply the changes. The newly created Library Item should now appear in the second slice.
  6. Next, navigate to **Developer | Page Definitions**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41330806358291)  
  

  7. Within the first slice, click the Shared JS option under the Actions section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41330806359187)  
  

  8. Within the editor, use the following code to reference the sound file stored as a Library Item:  
  

         
         ets.ready(function (page) {
           page.notificationAlert.on('alertCountChanged', function (model) {
         
             // check if the user has unread notifications
             if (model.numUnread > 0) {
               // get audio and play
               // This Assumes a Library Item called 'notification.mp3' exists in a Library Group with a Key of 'sounds'
               var audio = new Audio(ets.rootPath + '/library/' + page.pages.currentSiteKey + '/sounds/notification.mp3');
               audio.play();
             }
           });
         });
         

  
As mentioned in the code comments, the URL used to reference the Library Item uses the names provided in this example. If different names are used, the URL will need to be updated to accommodate the differences.  
  

  9. Click Save & Close on the editor to apply the changes.
  10. Finally, the solution can be tested by sending a Notification Alert. To do so, navigate to **Configuration | Notifications**.
  11. Select the desired Notification Definition Group and Notification Definition on the first and second slices, respectively.
  12. On the third slice, click the Test button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41330771460499)  
  

  13. On the resulting page, enter the Username of the account that will receive the Alert. When it is successfully sent, the Alert will appear on the top right corner of the page and the notification sound should play.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/41330771462035)



While the steps above implement this sound globally for all pages in the TrakSYS Web, the solution can also be implemented within different parts of the Page Hierarchy. For example, a different sound file can be referenced at the Section level. If the code is placed within the Shared JS tab of the Section, only pages under that Section will play that specific sound file. Alternatively, similar code can be placed within the JS tab of individual pages. This will ensure that a specific sound will only play if the user is currently viewing that page.

**Note** : The JavaScript code should not be applied to a single page multiple times as this will attempt to play multiple sound files all at the same time. For example, if a single page inherits JavaScript code from the page above it using the Shared JS tab and the page also references a separate sound file from the JS tab, both sound files will be played simultaneously when an Alert is received.

### Playing Sounds for Toast Notifications (TrakSYS 12.0.2+)

This functionality can be extended to Toast Notifications. Similar to the example in the previous section, JavaScript code can be added to play a sound each time a Toast Notification appears on the page. The following example assumes the steps in [**this article**](https://portal.parsec-corp.com/hc/en-us/articles/28480693428115-Configuring-Toast-Notifications) have been followed.

When creating the Toast Notification in JavaScript code, it is possible to reference a sound file stored as a Library Item using the `Audio()` Constructor. It has a `play()` method that can be called to play the audio as the Toast Notification is generated. The following code example shows how this can be implemented. The Library Item URL in the previous section is also being used in this example:
    
    
    function showToast() {
      const options = {
          caption: 'TrakSYS Advanced Notification',
          body: 'Customized Toast Notification',
          theme: 0 /*  0 - none | 1 - primary | 2 - success | 3 - danger */,
          autoHideSeconds: 10,
          iconCss: 'bi-bell-fill',
          isBodyRawHtml: false,
          extraCss: ''
       };
      // Create the Toast Notification
      ets.ui.showAdvancedToast(options);
    
      // Reference the sound file stored as a Library Item.
      // The URL assumes that the Site Key is "home"
      var toastSound = new Audio(ets.rootPath + '/library/home/sounds/notification.mp3');
      // Play the sound after the Toast Notification is created.
      toastSound.play();
    }
    

Now when a Toast Notification is displayed, the sound file will also be played.

![](https://portal.parsec-corp.com/hc/article_attachments/41429932594323)

Similar to the previous section, the same JavaScript code should not be applied multiple times to a single page. Otherwise, multiple sound files (or the same sound file) will be played simultaneously as the Toast Notification appears.
