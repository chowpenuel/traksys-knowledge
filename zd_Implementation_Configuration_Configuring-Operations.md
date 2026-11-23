# Configuring Operations

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007953534-Configuring-Operations*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

Operations can be used to create custom links to other pages. These links will appear under the properties menu (typically on the third slice) when selecting a specific entity. This can be useful for providing extra navigation and custom options when configuring entities within the TrakSYS Web. When creating an Operation, there are three types that are available: Custom Operations, Common Operations, and Other Operations. 

  * The links that are generated for **Custom Operations** will appear under a section called “Custom” when an entity is selected. This section will appear once a Custom Operation has been created. If no Custom Operations exist, then this section will not appear when configuring an entity.
  * The links that are created for **Common Operations** will appear under the name of the selected entity. This is generally where the default Edit button will appear for the entity.
  * The links that are displayed when using **Other Operations** will always appear under the Actions section of a selected entity (typically on the third slice).



All three types of Operations can be configured within the TrakSYS Web under **Developer | Operations**. Additional technical information about Operations can be found in the [TrakSYS Reference Documentation](https://docs.parsec-corp.com/tsweb/custom-operations) section of the support site. This article explains the standard procedure for creating a Custom Operation within the TrakSYS Web.

### **Procedure**

The example shown below shows how to configure a Custom Operation for the Schedule entity.However, this method can also be used for other entities and types of Operations. A complete list of entity names are available in the Custom Operations article under the TrakSYS Reference Documentation section mentioned above in the **Summary** of this article.

  1. In the TrakSYS Web, navigate to **Developer | Operations**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18725387139859)  
  

  2. Click the New button under Entity Operations section in the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18725391395987)  
  


  3. On the resulting page, enter a Name and Entity under the appropriate fields. For this example, the Schedule entity will be used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18725443548563)  
  

  4. In the Data field, XML can be inserted to create the desired Operation. In the example below, a Custom Operation has been created and is linking to a custom Visual Page Definition with a Key of "advschededit."  
  

         
         <Operations>
          <Custom>
           <Operation Caption="Advanced Edit" Icon="far fa-pen-to-square" Url="~/pages/home/advschededit/">
            <Param Name="ID" Value="{ID}" />
           </Operation>
          </Custom>
         </Operations>

  
As shown in the example above, the parameters for the Caption, Icon, and Url can all be specified within the Operation tag.  
  

     * The **Caption** parameter is the name of the link that will appear when the user views the available option within the TrakSYS Web.
     * The **Icon** Parameter specifies the icon that will appear next to the link when it is displayed.
     * The **Url** Parameter specifies the page that the user will be redirected to when the link is clicked.
The **Param** tag can be used to pass additional parameters into the target page. A Param tag can be created for each parameter that will be passed into the target page. These tags can reference values that are available in the Values Dictionary of the source page.  
  
Since the Custom Operation in this example is using the Schedule entity, the "ID" parameter for the Schedules page (under **Configuration | Schedules**) will contain the ScheduleID of the selected Schedule. This parameter will be passed into the target page when the user clicks the link.  
  

  5. The final result should look similar to what’s shown below:

  
![](https://portal.parsec-corp.com/hc/article_attachments/18725661804947)  
  

  6. Click Save to apply the changes.
  7. The Custom Operation should now be listed under the properties of the entity when it is selected. Since the Schedule entity was used in this example, the generated link should now be visible when a user navigates to **Configuration | Schedules** and selects a configured Schedule.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18725691326483)  
  

  8. When a user clicks the link, they should be redirected to the page specified in the Url parameter of the Operation tag. Also, any parameters that are included in Param tag(s) should also appear in the query string of the target page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18725784881555)  
  




When configuring a Common or Other Operation, the XML code example shown in this article can also be used. However, the "Custom" tag shown in the example would have to be changed to either "Common" or "Other" to create the respective Operation. XML examples of these Operations and their results are shown below:

#### **Common Operation**
    
    
    <Operations>
     <**Common** >
      <Operation Caption="Advanced Edit" Icon="far fa-pen-to-square" Url="~/pages/home/advschededit/">
       <Param Name="ID" Value="{ID}" />
      </Operation>
     </**Common** >
    </Operations>
    

![](https://portal.parsec-corp.com/hc/article_attachments/18725881809043)

#### **Other Operation**
    
    
    <Operations>
     <**Other** >
      <Operation Caption="Advanced Edit" Icon="far fa-pen-to-square" Url="~/pages/home/advschededit/">
       <Param Name="ID" Value="{ID}" />
      </Operation>
     </**Other** >
    </Operations>
    

![](https://portal.parsec-corp.com/hc/article_attachments/18725899402515)
