# Using Custom Translations in JavaScript

*Source: https://portal.parsec-corp.com/hc/en-us/articles/32404940694803-Using-Custom-Translations-in-JavaScript*
*Last updated: 2025-05-21T22:07:50Z*

---

Applies To | TrakSYS 12.0.3+

### Summary

TrakSYS 12.0.3 added the ability to use Custom Translations in JavaScript. This is useful for displaying dynamic JavaScript text based on the configured Custom Translations and the user's locale. When this feature is enabled, it will make configured Custom Translations available to front end JavaScript code on every page within the TrakSYS Web. The TrakSYS API can be used to retrieve these values so they can be used and displayed within various JavaScript elements.

In order to use this feature, [Custom Translations](https://portal.parsec-corp.com/hc/en-us/articles/360007652173-Implementing-Custom-Translations) must be created along with the respective Locales. The example in this article assumes that Custom Translations already exist within the configuration. The configuration used is a continuation from the example used in the "Implementing Custom Translations" article linked above.

### Making Translations Accessible to JavaScript

When configuring Custom Translations, there is a new option available for Resource Groups called Translation Mode. This option can be accessed by going into the configuration of a Resource Group and navigating to the General tab.

![](https://portal.parsec-corp.com/hc/article_attachments/32431047679251)

This option will have three different values explained below:

  * **All** \- When selected, Custom Translations under this Resource Group will be available to elements that are server-side and client-side.
  * **Server Only** \- When selected, Custom Translations will only be available to server-side elements. This includes Content Parts, Content Pages, and C# page scripting. This is the default option when creating new Resource Groups.
  * **JavaScript Only** \- When selected, Custom Translations will only be available to client-side elements. In other words, they will only be accessible through custom JavaScript code on pages.



Choosing the Server Only or JavaScript Only options can be useful for organizational purposes. However, this assumes that it is known whether all Custom Translations for a Resource Group will only be used for server-side or client-side purposes. If this information is not known, it is recommended to choose the All value. For the purpose of this example, all Resource Groups will be configured to use All.

### Checking The Available Client-Side Translations

Once a Resource Group is configured to use JavaScript Only or All and Custom Translations have been created, it is possible to check which translations are now available to use for client-side purposes. The following steps describe how to do this:

  1. While viewing any page within the TrakSYS Web, press F12 to open the browser Developer Tools.
  2. Select the Console option within the navigation menu. **Note** : this menu may look slightly different depending on which browser is used. In the screenshot below, the Google Chrome browser is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32431374086675)  
  

  3. Within the Console, type `etsresx.custom` and press enter.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32431341335443)  
  

  4. Expand the tree of options that appears below the command. This will show a full list of the available Keys for configured Resource Groups and Custom Translations.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32431940624915)  
  

  5. The top level Keys represent the Keys used in each configured Resource Group. The child entries represent the Keys used for the individual Custom Translations along with the exact strings that will be translated. In the example below, 2 Resource Groups have been configured along with a single Custom Translation per Group. If more Translations and Groups have been configured, they should be displayed within the results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32432121741971)



### Referencing Custom Translations in JavaScript

The following steps show how to access Custom Translations using client-side JavaScript code in a Visual Page Definition. Additional Parts are used in the example to display the resulting value, but are not required when using this functionality.

  1. Navigate to **Developer | Page Definitions** and create a new Visual Page Definition.
  2. Access the Parts tab and add a Buttons Part (`ETS.TsButtons`) to the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32433910667283)  
  

  3. For the purpose of this example, the following settings are being used:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32433910668947)  
  

  4. Once the button has been configured, click the ellipsis (...) to open the Click Actions menu.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32433894536595)  
  

  5. Within the On Client Click field, specify a function name. This will be used to reference a function that will be created in JavaScript code. For this example, "myFunction()" is being used. In actual implementations, it is recommended to use more meaningful names.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32433894544019)  
  

  6. Click OK and save the changes to the Part.
  7. Next, navigate to the JS tab of the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32433894549779)  
  

  8. To retrieve the value for a Custom Translation in client-side code, the following call can be used (where ResourceGroupKey is the actual Key used for the configured Resource Group and ResourceItemKey is the actual Key used for the configured Resource Item):  
  

         
         etsresx.custom.ResourceGroupKey['ResourceItemKey']
         

  
Therefore, based on the configuration of this example, the following JavaScript function can be used to retrieve the Custom Translation:  
  

         
         function myFunction()
         {
           ets.ui.alert(etsresx.custom.ReportTrans['Translation']);
         };
         

![](https://portal.parsec-corp.com/hc/article_attachments/32433894559635)  
  




At this point, the changes can be saved and the page can be previewed. Based on the full configuration of this example, the page will look similar to the following:

![](https://portal.parsec-corp.com/hc/article_attachments/32433910710931)

Since the translation string was originally created in English, a user with an English locale (such as en-US) will see the original string when the button is clicked.

![](https://portal.parsec-corp.com/hc/article_attachments/32433910717843)

However, if a different user with a configured locale accesses the page and clicks the button, they should now see the corresponding translation based on the detected locale. For this example, translations have been created for the Spanish (es-ES) and French (fr-FR) locales. Users with these locales should see the following when the button is clicked. **NOTE:** If you do not see the translations right away, log out of the TrakSYS Web and log back in with a user that matches the corresponding locale.

**Spanish Translation**

![](https://portal.parsec-corp.com/hc/article_attachments/32433894585491)

**French Translation**

![](https://portal.parsec-corp.com/hc/article_attachments/32433894591379)
