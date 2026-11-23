# Configuring and Using Fast Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500005907182-Configuring-and-Using-Fast-Tags*
*Last updated: 2025-05-21T22:43:12Z*

---

Applies To | TrakSYS 11.2.0+

### **Summary**

TrakSYS 11.2.0 introduced Fast Tags, which allow displaying rapid UI updates from Tag values (OPC DA, OPC UA, and Smart Devices). They are ideal for real-time observation and decision-making displays that change with sub-second frequency. This article explains how to configure and use Fast Tags.

### **Procedure**

#### **Configuring Fast Tag Sets and Fast Tags**

  1. In the TrakSYS Web, navigate to **Configuration | Tags | Fast Updates**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18652192613523)  
  

  2. Under the Sets section, click New on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18652246679699)  
  

  3. On the resulting page, specify a Name and Key for the Fast Update Set. Then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18652285423763)  
  

  4. Select the newly created Fast Update Set and click New under the Fast Tags section in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18652310359059)  
  

  5. On the resulting page, enter a Name and select the desired tag for the Source Tag property. Then, click the Save button. Note that only OPC DA, OPC UA, or Smart Tags can be selected. For the purpose of this example, an OPC UA tag is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18652363271955)  
  

  6. Repeat steps 4 and 5 to add additional Fast Tags as needed.



### **Using Fast Tags**

There are two ways to display Fast Tag values on a page: in a Gauge Content Part (configuration only) or via Tag Format expressions (programmatic).

#### **Gauge Content Parts**

These parts can be configured to use Fast Tags as the data source.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18652419233811)

#### **Tag Format Expressions**

Fast Tag values can be displayed using [Tag Format](https://docs.parsec-corp.com/tsweb/expression-syntax/format/tag-format) in any expressionable Content Part, with the prerequisite that a subscription to the Fast Tag Set must be created programmatically.

This subscription can be done in any `PreInit` method that is appropriate for the Content Part being used to display the values (e.g. `ContentPage_PartPreInit02()`, `ContentPage_PartPreInit05()`, etc., or simply in `ContentPage_Init()`).

In the example below, the Fast Tag Set subscription is done in the `ContentPage_Init()` method. It is referencing a Fast Tag Set Key of `ProdFastUpdate`.
    
    
    protected override bool ContentPage_Init()
    {
      // Get the current SiteID
      int siteID = this.Ets.Values.GetAsInt("ETS.SiteID");  
    
      // Load the Fast Tag Set using the Key and SiteID
      var fastSet = this.Ets.Api.Data.DbFastUpdateSet.Load  
                    .ByKeyAndSiteID("ProdFastUpdate", siteID)  
                    .ThrowIfLoadFailed("Key", "ProdFastUpdate");
    
      // Returns the FastUpdateSet key
      this.Ets.Js.SubscribeToFastUpdateSetByID(fastSet.ID).ThrowIfFailed();
      return true;
    }
    

Once the subscription is complete, [Tag Format](https://docs.parsec-corp.com/tsweb/expression-syntax/format/tag-format) can be used to reference individual tags by Name or ID. For the `tagname` Tag Format expression, the corresponding Values Dictionary key must reference the value of `tTag.Name`. The Values Dictionary key can be specified in the appropriate `PreInit` method for each part or it can be placed in `ContentPage_Init()`.

In the example below, the tag name is being inserted into the Values Dictionary to reference the OPC UA tag assigned to the Fast Tag Set.
    
    
    this.Ets.Values["UATag"] = "OPC UA Tag";
    

The tag can now be referenced using the Tag Format expression, for example, in the Text property of a Header Part.

![](https://portal.parsec-corp.com/hc/article_attachments/18652566883731)

The tag's value will now display on the page, updating at sub-second frequency (provided the source tag is doing so).

![](https://portal.parsec-corp.com/hc/article_attachments/35342723295763)
