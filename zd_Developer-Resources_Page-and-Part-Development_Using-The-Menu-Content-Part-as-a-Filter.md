# Using The Menu Content Part as a Filter

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001352494-Using-The-Menu-Content-Part-as-a-Filter*
*Last updated: 2025-05-21T22:53:43Z*

---

Applies To | TrakSYS 10+

The Menu Content Part (`TsMenu`) can be used as an alternative to the Filter Drop Down (`Filters.TsFilterDropDown`). This topic illustrates how to use the Menu Part in this way.

### **Example**

The following example shows how to create a filter with 3 options (Normal, Warnings and Past Due). The page will show the appropriate menu item as selected and helps to differentiate the value of the _Key_ versus the text display presented to the user. The example also uses a Paragraph Content Part to display the results of the filter, but in practice these results can be used in code or as the source of Content Properties to properly query or show data.

  * Create a Visual Content Page
  * Add a `Paragraph` Content Part
  * Set the Text property to:


    
    
    The current mode is {mode[normal]}  //expression for Values Dictionary key called "mode" and default value of normal 

  * Add a `Menu` Content Part with Part ID of `Mode`. **IMPORTANT:** The ID of the Content Part must be accurate, it controls what menu item will be shown as selected.
  * Add 3 Menu Items with the following values: 
    * _Key_ = normal : _Caption_ = Normal
    * _Key_ = warnings : _Caption_ = Warnings
    * _Key_ = over : _Caption_ = Past Due
  * Set the Default Selected Item to "normal" (this matches the _Key_ of the first Menu Item).
  * For the 3 Menu Items, access the link properties by clicking the ellpsis (...) and set the URL to the following values: 
    * self:mode=normal
    * self:mode=warnings
    * self:mode=over
  * Save and/or Preview the results



### **Advanced**

The self URL syntax of `self:Key1=Value1&Key2=Value2` can be used anywhere a URL needs to be provided. If a URL starts with the prefix `self:` then the current URL will be used as a base, leveraging the current Query String (i.e. `this.Ets.QueryString`) and either adding new Query String values based on the `self:` url or overriding existing values. Essentially, the following method is called:
    
    
    this.Ets.Pages.BuildSelfUrlIfNecessary("self:Key1=Value1");
    

An example of this in practice is the trace eyeball in the page footer, which essentially is just the string `"self:trace=1"` or `"self:trace=0"` depending on the current value.
