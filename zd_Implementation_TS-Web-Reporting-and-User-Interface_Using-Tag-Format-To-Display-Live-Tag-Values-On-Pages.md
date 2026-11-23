# Using Tag Format To Display Live Tag Values On Pages

*Source: https://portal.parsec-corp.com/hc/en-us/articles/34695875626387-Using-Tag-Format-To-Display-Live-Tag-Values-On-Pages*
*Last updated: 2025-05-21T22:34:48Z*

---

Applies To | TrakSYS 11+

### Summary

In some cases, it may be desirable to display live Tag values for pages meant to display real-time data. To meet this requirement, TrakSYS uses the [Tag Format](https://docs.parsec-corp.com/tsweb/expression-syntax/format/tag-format) syntax to display values. This syntax takes the Tag Name or Tag ID stored within the Values Dictionary and uses JavaScript code to display live, updating Tag values. By default, this functionality refreshes the Tag value once every second. This interval can be increased if [Fast Tags](https://portal.parsec-corp.com/hc/en-us/articles/1500005907182-Configuring-and-Using-Fast-Tags) are configured and used with Tag Format Syntax. This article contains an example of how the Tag Format Syntax can be used.

### Example

This example shows one possible use of the Tag Format syntax. The syntax can be used in other Parts as well.

  1. Within a new Visual Page Definition, navigate to the Script tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34698299852179)  
  

  2. Within the `ContentPage_Init()` method, insert the desired Tag Name or Tag ID to be used with the Tag Format syntax into the Values Dictionary. While any Key name can be used, "UpdatingTagName" is used as the Key for this example. The code example below uses the Tag Name, but provides an option for Tag ID if needed.  
  

         
         protected override bool ContentPage_Init()
         {
           //Insert Tag Name into Values Dictionary
           this.Ets.Values["UpdatingTagName"] = "OPC UA Tag";
           //Uncomment line below to Insert TagID into Values Dictionary instead
           //this.Ets.Values["UpdatingTagID"] = //Your TagID Here
           return true;
         }
         

  3. After saving the changes, navigate to the Parts tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34698361170451)  
  

  4. Add a Header Part (`ETS.TsHeader`) to the page.
  5. Within the properties of the Part, the Tag Format syntax was used to reference the Values Dictionary Key containing the Tag Name:  
  

         
         {UpdatingTagName:tagname}
         

  
![](https://portal.parsec-corp.com/hc/article_attachments/34709196389651)  
  
If the option for Tag ID is used, the syntax would be similar to the following:  
  

         
         {UpdatingTagID:tagid}

  6. After saving the changes and previewing the page, the Header should show the live tag value changes. The values will update once per second:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/35339768198163)



As an extension to this concept, it is possible to place the Tag Format syntax within strings of text to make it more user friendly. Continuing from the example, the following value was placed within the Text field of the Header Part:

![](https://portal.parsec-corp.com/hc/article_attachments/34709498500883)

Upon saving the changes and previewing the page, the Tag should still provide live value updates within the full string:

![](https://portal.parsec-corp.com/hc/article_attachments/35339869054099)
