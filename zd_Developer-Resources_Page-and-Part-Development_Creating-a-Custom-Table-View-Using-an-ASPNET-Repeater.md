# Creating a Custom Table View Using an ASP.NET Repeater

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360035450514-Creating-a-Custom-Table-View-Using-an-ASP-NET-Repeater*
*Last updated: 2025-05-21T22:52:38Z*

---

Applies To | TrakSYS 10+

### **Summary**

The Table View part includes properties that allows developers to customize the HTML table rendered in the UI. However, there may be business requirements that the built-in table view currently does not support (e.g. column sorting). For these types of situations, it's necessary to develop a custom table view in order to implement the desired functionality.

This sample will provide a bare-bones template for creating a custom table within a View Fragment part and how to link data from a custom query.

### **Example**

In the Parts section of the Page Definition, add a Custom SQL Data Table and insert the following query.
    
    
    SELECT
       EventID,
       EventDefinitionName,
       DurationSeconds
    FROM   
       viewEvent
    

![](https://portal.parsec-corp.com/hc/article_attachments/18995584910483)

Under the Data tab, enter a unique _Target Values Key_. This key will be used as a reference in a later step.

![](https://portal.parsec-corp.com/hc/article_attachments/18995633081747)

The following code is the markup and visual customization of the table entered in the View Fragment part. It leverages ASP.NET’s **Eval()** method to bind data to the UI control. The code also contains CSS Classes that will duplicate the look and feel of a built-in table view. 
    
    
    <div class="col-sm-12 tscontentpart-dynamic">
     
     <asp:repeater id="repeaterEvents" runat="server">
       <headertemplate>
         <table class='table table-striped'>
           <thead>
             <tr> 
              <th>Event ID</th>
              <th>Event Name</th>
              <th>Duration Seconds</th> 
            </tr>
          </thead>
         <tbody>
      </headertemplate>
      <itemtemplate>
            <tr class='tsrow-hoveronly'> 
             <td><span><%# Eval("EventID") %></span></td>
             <td><span><%# Eval("EventDefinitionName") %></span></td>
            <td><span><%# Eval("DurationSeconds") %></span></td> 
          </tr>
     </itemtemplate> 
     <footertemplate>
         </tbody>
        </table>
     </footertemplate>
     </asp:repeater>
     
    </div>
    

Navigate to the Script Editor and enter the code below under _ContentPage_PartPreInit10()_.
    
    
    protected override bool ContentPage_PartPreInit10()
    {
      string errorMsg = "Unable to load Data.CustomEvent Data Table";
      // retrieve custom data table
      var dt = this.Ets.Values.GetAs("Data.CustomEvent",new DataTable()).ThrowIfNull(errorMsg);
    
      //bind datasource to ASP Repeater 
      this.repeaterEvents.DataSource = dt;
      this.repeaterEvents.DataBind();
    
      return true;
    }
    

The final output of the custom table should look similar to the following.

![](https://portal.parsec-corp.com/hc/article_attachments/18995859493523)
