# Using Phantom Instancing

*Source: https://portal.parsec-corp.com/hc/en-us/articles/40814531532307-Using-Phantom-Instancing*
*Last updated: 2025-05-30T22:52:01Z*

---

Applies To | TrakSYS 13+

### Summary

Starting in TrakSYS 13, a new functionality called **Phantom Instancing** is available. This feature allows instance keys to be applied directly to Page Definitions at multiple navigation levels without requiring traditional instance properties. The result is a more flexible and dynamic instancing mechanism.

Creating instance keys with Phantom Instancing enables but is not limited to the following benefits:

  * Redirecting to a configured Visual Page or Content Page via Page Script or the Content Part URL property, while applying instancing.

  * Defining logic based on the presence or absence of a Phantom Instance Key.

  * Allows users to handle scenarios where a Phantom Instance Key contains an unexpected value.

  * Avoiding the creation of separate pages in the navigation tree per instance.




**Note** : It is not possible to apply Phantom Instancing to Pages that already leverage another form of instancing.

### Syntax and Explanation

Phantom Instancing uses the following syntax to define instance keys:
    
    
    $<InstanceKeyHere>

Unlike other forms of instancing, Phantom Instancing can be used in all areas of the page hierarchy (including Section pages). The following is a simple example of using Phantom Instancing at the Section level:
    
    
    http://servername/ts/pages/sitekey/section$instancekeyhere

Additionally, Phantom Instancing can be used at multiple levels of the URL. This can be useful when creating dynamic URLs that include multiple pages for specific entries. The following example shows Phantom Instancing at the Section, Hub 1, Hub 2, and Hub 3 levels within a single URL:
    
    
    http://servername/ts/pages/sitekey/section$SectionKey/hub1$KeyOne/hub2$KeyTwo/hub3$KeyThree

Note that when using the Phantom Instancing feature, the dollar sign "$" must directly follow the page Key. It cannot contain a forward slash character "/" between the Key and the dollar sign. For example, **the following is incorrect and will cause the page to produce an error message:**
    
    
    http://servername/ts/pages/sitekey/section**/$** instancekeyhere

Similar to the existing instancing options, the intention is that Phantom Instancing will be leveraged in the Values Script. This is separate from the normal C# code editor in a Page Definition. In the Values Script, the following string object in the form of a local variable is available:
    
    
    instanceKey

Note that only the Instance Key at the current Page Hierarchy will be accessible. Therefore, the intended approach is to set configure the Values Script instancing logic on a per-page Hierarchy level.

Additionally, the instances are accessible in the C# Script Editor under the following properties:

  * this.Ets.Pages.Section.InstanceKey
  * this.Ets.Pages.Hub1.InstanceKey
  * this.Ets.Pages.Hub2.InstanceKey
  * this.Ets.Pages.Hub3.InstanceKey



### Example

To demonstrate the functionality, the following Section was created as a Visual Page:

![](https://portal.parsec-corp.com/hc/article_attachments/41676396305171)

The following code is placed in the Values Script:
    
    
    if (instanceKey.IsNotNullOrWhiteSpace())
    {
      // perform instancing logic here
      values["Sys.Key"] = instanceKey;
    }
    
    return Result<bool>.ReturnSuccessfulResult(true);

While viewing the Section page, an instance can be created through Phantom Instancing:

![](https://portal.parsec-corp.com/hc/article_attachments/41676380019091)

The Page Trace should now show the Section Instance Key and be accessible through the Values Dictionary:

![](https://portal.parsec-corp.com/hc/article_attachments/41676380020115)

This Key can be referenced through the Values Script, C# Script, or by other Parts for extensibility purposes.
