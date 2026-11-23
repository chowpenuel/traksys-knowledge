# Configuring Toast Notifications

*Source: https://portal.parsec-corp.com/hc/en-us/articles/28480693428115-Configuring-Toast-Notifications*
*Last updated: 2025-05-21T22:34:56Z*

---

Applies To | TrakSYS 12.0.2+

### Summary

Starting in TrakSYS 12.0.2, a new type of notification called Toast Notifications was added. These notifications can be used to send on-screen messages to provide alerts or informational status updates to users. These messages will appear on the bottom right corner of the page to get the user's attention. The notifications can be customized to alter the look and content as needed. This article contains an example of how Toast Notifications can be used on a page and contains more information about the available options as well as Toast Notification behavior.

### Example

The following example uses a Visual Page Definition with a Buttons Part to generate the Toast Notifications. This example shows how to generate a simple Toast Notification with default settings and an advanced Toast Notification, which has additional options to customize notification content.

  1. Within the TrakSYS Web, navigate to **Developer | Page Definitions** and create a new Visual Page Definition.
  2. Once the page has been created, click the Parts link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28755945213331)  
  

  3. Add a Buttons Part (ETS.TsButtons) to the page. Ensure that two buttons have been added to the Part. For this example, the following settings have been applied:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28755945235731)  
  

  4. For the first button, click the ellipsis (`...`) to open the Click Actions menu.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28755945242131)  
  

  5. Within the On Client Click option enter the following line of JavaScript code. This method will show a simple Toast Notification with default settings  
  

         
         ets.ui.showToast('TrakSYS Notification', 'Test Toast Notification')

  
![](https://portal.parsec-corp.com/hc/article_attachments/28755966589843)  
  

  6. Save the changes.
  7. Next, click the ellipsis (`...`) for the second button to open the Click Actions menu  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28756518502803)  
  

  8. In the On Client Click option, enter a method that will be used to trigger the Toast Notification. The JavaScript code for the method will be included in the next steps. For the purpose of this example, the method name "`showToast()`" is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28756531374739)  
  

  9. Save the changes within the Click Actions menu and for the Buttons Part.
  10. Then, navigate to the JS editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28756531378707)  
  

  11. Within the JavaScript editor, the following code is being used. A full explanation of the available settings will be provided in the next section of this article.  
  

         
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
           ets.ui.showAdvancedToast(options);
         }
         

![](https://portal.parsec-corp.com/hc/article_attachments/28756960131603)  
  

  12. Save the changes and Preview the page. Both buttons should be present on the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28774332853267)  
  

  13. Click the Toast button to generate a simple Toast notification. As shown below, this type of notification will use predefined settings to generate Toast messages. The messages will always use the Primary (blue) color and can only display string text in the description of the message.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28774332865427)  
  

  14. Once the message disappears or is dismissed, click the Advanced Toast button. This notification is generated based on the values provided in the advanced settings available within the `showAdvancedToast()` JavaScript method. A full explanation of these settings is provided in the next section of this article. As shown below, the advanced Toast Notification appears in a different color specified by the `theme` option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/28774714720659)



#### Advanced Toast Settings

The `ets.ui.showAdvancedToast()` JavaScript method contains several options to further customize the Toast Notifications. A description of each setting is provided below:

The **caption** option specifies the line of text that will be displayed on the top of the Toast Notification. Since this is a string value, a hard-coded string or a dynamically changing string variable can be used for this option.

The **body** option specifies the content that will be displayed within the main body of the Toast Notification. A hard-coded string or a dynamically changing string variable can be used for this option. Depending on the isBodyRawHtml option, HTML content can also be included (more information about this is explained for the isBodyRawHtml option below).

The **theme** option accepts enumeration values that control the color and styling for the Toast Notification. The available values for this option are shown below:

  * 0 - None
  * 1 - Primary
  * 2 - Success
  * 3 - Danger



The styling for each of these options is shown below. Note that if the `ets.ui.showToast()` method is used to generate simple Toast Notifications, it will use the Primary theme by default.

![](https://portal.parsec-corp.com/hc/article_attachments/28775886661267)

The **autoHideSeconds** option specifies the number of seconds that the Toast Notification will be displayed on the page before it is automatically dismissed. If the `ets.ui.showToast()` method is used, all notifications will be automatically dismissed after 10 seconds.

**NOTE** : The minimum value for this field is 10 seconds. If a value between 1 and 10 is provided, this setting will automatically default to 10 seconds. Additionally, providing a value of 0 or -1 in this field turns off the auto hide functionality. If this is the case, notifications will not disappear and must be manually dismissed.

The **iconCss** option specifies the icon that will be used for the Toast Notification. This option accepts any built-in CSS class that references a TrakYS Icon. If nothing is specified for this field, then no icons will be included in the notification. By default, notifications generated by the `ets.ui.showToast()` method do not have icons.

The **isBodyRawHtml** option accepts a Boolean value of true or false, which specifies whether the body content of the Toast Notification contains HTML. If a value of true is provided, it will process all HTML included in the body and display it accordingly. 

As an example, the following code is being used to generate a Toast Notification:
    
    
    function showToast() {
      const options = {
          caption: 'TrakSYS Advanced Notification',
          body: 'This is <strong>bold text</strong>.<br/> This is <em>italicized text</em>.<br/> <a href="https://portal.parsec-corp.com/">TrakSYS Support Site</a>',
          theme: 0 /*  0 - none | 1 - primary | 2 - success | 3 - danger */,
          autoHideSeconds: 10,
          iconCss: 'bi-bell-fill',
          isBodyRawHtml: true,
          extraCss: ''
       };
      ets.ui.showAdvancedToast(options);
    }
    

As shown, the body parameter includes multiple different HTML tags for styling. Additionally, the isBodyRawHtml option is set to true. When the notification is generated, all of the HTML is correctly rendered as expected:

![](https://portal.parsec-corp.com/hc/article_attachments/28782179260307)

The **extraCss** option allows extra CSS classes to be applied to the Toast Notification. Any styling provided by these classes will be applied in addition to the theme.

### **Success Toast Notifications Across Pages (TrakSYS 13+)**

Starting with TrakSYS 13.0.0, it is now possible to create Toast Notifications across pages with the following method:

###  this.Ets.Pages.SetNextPageToast()

Most of the `showAdvancedToast` options (shown in the previous section) appear as parameters in this method. In place of the theme option, there is a parameter that takes in a `JsToastTheme` Enum that behaves similarly. As an example, the following code is being used to generate the Toast Notification on another page:
    
    
    protected void ToastRedirect(object sender, EventArgs e)
    {
      this.Ets.Pages.SetNextPageToast("Toast Body", "Toast Caption", ETS.Ts.Core.Enums.JsToastTheme.Success, /*autoHideToastSeconds*/ 10, "fa-thumbs-up");
      this.Ets.Pages.RedirectToSuccessUrl();
    }
    

When the user is redirected to the target page, the Toast Notification will appear indicating success (or failure).

![](https://portal.parsec-corp.com/hc/article_attachments/41438603811347)

### Toast Notification Behavior

#### Extending Auto-Hide With On-Hover

When creating Toast Notifications, each message will be automatically dismissed after a period of time. If the `ets.ui.showToast()` method is used, all generated messages will disappear after 10 seconds. All Toast Notifications generated by the `ets.ui.showAdvancedToast()` method will disappear after the user-defined value in the autoHideSeconds property. In both cases, a user can extend the timeout by hovering over the notification. As long as the mouse is hovering over the notification, it will be displayed indefinitely. As soon as the user moves the mouse off of the notification, the auto hide timer will continue and will eventually be dismissed.

#### Displaying Multiple Toast Notifications

In some cases, it may be desirable to display multiple Toast Notifications at the same time when a user views a page. In this case, multiple notifications will be stacked vertically starting from the bottom right corner of the page. Older notifications will be pushed to the top of the stack as newer notifications are generated:

![](https://portal.parsec-corp.com/hc/article_attachments/28783499255827)

Each notification will use it's own auto hide timer and will be automatically dismissed based on when it was created. As mentioned in the section above, this timeout can be extended by hovering over the notification. When this happens while multiple messages are displayed, only the message that is being hovered over will have an extended timeout. As notifications are dismissed, the stack of notifications will fall to the bottom of the screen. Notifications that are dismissed in the middle of the stack will shift notifications above it downwards.
