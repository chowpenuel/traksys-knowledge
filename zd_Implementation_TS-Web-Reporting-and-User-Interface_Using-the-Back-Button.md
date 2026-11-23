# Using the Back Button

*Source: https://portal.parsec-corp.com/hc/en-us/articles/50695411857683-Using-the-Back-Button*
*Last updated: 2026-04-20T21:55:47Z*

---

Applies to | TrakSYS 14.0.0+

### Summary

In TrakSYS 14.0.0, Back Button functionality was introduced, providing a standardized, built-in method for adding a Back Button to pages. The feature also includes options for customizing the button’s appearance and supports the exclusion of specific URLs to enable more granular control over navigation behavior. This article outlines the steps required to configure the Back Button, explains the available configuration options, and provides examples demonstrating how specific pages and URLs can be excluded from navigation.

### Configuring the Back Button

The following steps describe the standard procedure for enabling and configuring the Back Button. These steps can be used on both Visual Pages and built-in Content Pages.

  1. In the TrakSYS Web, navigate to **Developer | Page Definitions**.
  2. On the second slice, select the desired Page Definition. Then, click the Edit button on the third slice. In this example, a Hub 2 Visual Page Definition was selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50785707045395)  

  3. On the resulting page, navigate to the Back tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50785707046547)  

  4. This tab includes several options that can enable and customize the behavior of the Back button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50785707048339)  

     * **Back Visible** \- This option determines whether the Back button will be displayed on the current page. To display the button, this option should be set to True. If this property is set to True on a page further up in the hierarchy, then the Inherit option can be used instead.   
  
**NOTE** : This option requires Spokes to be visible for the page. If Spoke visibility is disabled, then the Back button will not be displayed even if this property is set to True.  

     * **Back Button Caption** \- This option specifies the Caption that is displayed on the Back button. If no value is provided the button will display "Back" for the button text.  

     * **Back Icon** \- Specifies the Icon CSS that will be used for the Back button. If no Icon is selected the "fa-circle-left" Icon CSS will be applied automatically.  

     * **Return URLs Excluded** \- This option specifies the list of URLs that should be excluded when the Back button is clicked. Multiple URLs can be included in this list with one URL per line (covered in the next section).  

  5. Once all changes have been applied and the page is previewed, the Back button should now display on the top right corner.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/50786265873811)  
  
**NOTE** : When the Back button is rendered, it will always appear on the top right corner of the page. It is currently not possible to modify the position of the button.  

  6. Repeat these steps for each page that should have the Back button enabled.



### Adding URL Exclusions

The configuration for the Back button allows specific URLs to be excluded. This is useful for scenarios where users should not be redirected to certain pages when clicking Back or if the Back button should only redirect users to a specific page. The following examples demonstrate how to exclude URLs to further refine how the Back button will function. For the purpose of these examples, pages have been configured using the following hierarchy:

  * Section : Line 1, Key : L1
    * Hub 1 : Packaging, Key : Pack
      * Spoke : Event List, Key : EvList
      * Spoke : OEE Report, Key : OEEReport



#### Excluding URLs

In this example, a user can navigate through the pages above using the following flow:

Line 1 -> Packaging -> Event List

Assuming that all pages have the Back button enabled, the user will be able to click it on the Event List page to get back to the Packaging page. However, if the same Back button is clicked on the Packaging page, it will redirect the user back to the Event List page as it was the last page visited. This effectively creates an unescapable navigation loop. To prevent this from occurring, the URL for the Event List can be provided in the list of excluded URLs. Based on the page hierarchy shown above, the following URL syntax is used:
    
    
    /TS/pages/{SiteKey}/{SectionKey}/{Hub1Key}/{SpokeKey}
    

Therefore, the following URL is provided:
    
    
    /TS/pages/home/l1/pack/evlist
    

![](https://portal.parsec-corp.com/hc/article_attachments/50792609882515)

When providing URL Exclusions, a URL must be proved for each page that should be excluded. Since there are two Spokes that are included under the Hub 1, a link for the second Spoke (OEE Report) will also need to be provided. This link uses the same syntax as the original link and is placed on its own line.

![](https://portal.parsec-corp.com/hc/article_attachments/50792639438995)

These steps will need to be repeated for each individual page that should have exclusions. Additionally, each individual exclusion will need to be added to every page that should have them. Because of this, it is recommended to use Wildcards (explained below) to help reduce the number of links that would need to be added.

#### Using Wildcards to Exclude URLs

When adding URL exclusions, it is possible to use a Wildcard to exclude specific elements from many different cases. It can also be used to shorten the URLs defined for the exclusions. A Wildcard is defined by the asterisk ( * ) character and can be placed before and after an element to exclude different elements within a URL. 

Continuing the example from the previous section, it is possible to exclude both Spokes from the navigation by placing an asterisk before the URL. This will exclude any URL that was used to navigate to that particular page. Therefore, the URLs will now look like the following:
    
    
    */evlist
    */oeereport
    

![](https://portal.parsec-corp.com/hc/article_attachments/50927029478419)

Additionally, the Wildcard can be placed in most areas of the URL to exclude specific Keys or even query string values. Some other uses for the Wildcard are shown below:

  * */PageKey/*



This will exclude all URLs that contain this specific Page Definition Key. This can be done at any level of the URL starting with the Section and below in the hierarchy.

  * /PageKey?*MyValue=1*



This will exclude a specific query string key-value pair from the URL.

  * /PageKey/*



This will exclude all URL elements in the hierarchy below the current Page Definition Key.

Multiple Wildcards can also be placed around multiple elements within the same URL. Doing so can help address very complex navigation requirements where users can only navigate back to very specific pages in specific scenarios. 
