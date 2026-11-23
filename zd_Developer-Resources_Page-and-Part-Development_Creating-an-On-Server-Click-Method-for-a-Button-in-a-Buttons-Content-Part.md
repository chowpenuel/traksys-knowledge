# Creating an On Server Click Method for a Button in a Buttons Content Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007516854-Creating-an-On-Server-Click-Method-for-a-Button-in-a-Buttons-Content-Part*
*Last updated: 2025-05-21T22:52:52Z*

---

Applies To | TrakSYS 10+

### **Summary**

A server-side method can be created by inputting the method name into the On Server Click field. Then, the method can be created in the code-behind of the Page Definition. Please note that this process can also be used for any part that contains an On Server Click field (e.g. Tiles, Table Views, Tree Views, List Views, etc.).

### **Procedure**

  1. In the Properties of the Buttons Part, navigate to the General tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18996677666963)  
  

  2. In a configured button, click the ellipsis (...) to bring up the Click Actions menu.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18996727212307)  
  

  3. In the On Server Click field, type the desired name of the OnClick method that will be used for the button. In the example below the method name Button_Click was inputted.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18996766608531)  
  

  4. Click OK. 
  5. Click Save to apply the changes.
  6. Next, navigate to the Script tab within the Page Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18996774488723)  
  

  7. Within the code editor, add the OnClick method for the button. Please note that the name of the method must match the method name entered in the On Server Click field in step 3.   
  

         
         protected void Button_Click(object sender, EventArgs e)
         {
           // Insert code here
         }
         

  8. Any code inserted into this method will now execute when the button is clicked.



#### **Differences in Method Signature**

While this process can be used for other built in Content Parts (like Tiles, Table Views, and List Views), the method signature may be different depending on which part is being used. 

More specifically, row-specific Content Parts like the Table View will require **RowItemEventArgs** instead of the typical EventArgs parameter for a Buttons Content Part. Therefore, a method for a button in a Table View should look similar to the following:
    
    
    protected void Button_Click(object sender, **RowItemEventArgs** e)
    {
      // Insert code here
    }

#### **Best Practices**

Typically OnClick methods do not have any error handling within them. If any exceptions are raised, the entire page will error and go to the error page. Therefore, it is recommended to add additional error handling (e.g. a try/catch block), especially if the code within the OnClick method is modifying data in the TrakSYS database. 

When adding error handling, it is also recommended to not ignore the result object. The result object can be checked using various methods within the API (e.g. the ThrowIfFailed() and ThrowIfLoadFailed() extension methods).

There are also several methods within the Ets.Debug namespace that can help catch and display errors when they occur. When using methods in the Ets.Debug namespace, the failure of the page will be determined by the **PageMode** setting in the TrakSYS Settings section of the TrakSYS Installation Manager (which can be set to **DebugMode** or **RedirectOnError**).

In the example below, an event is loaded using a Model Object. The Capture01 and IsEdited fields are then modified and the changes are pushed to the TrakSYS database. The example demonstrates the proper use of the ThrowIf extension methods and the try/catch block within an OnClick Server method:
    
    
    protected void Button_Click(object sender, EventArgs e)
    {
      try
      {
        // Create and populate the model object using the EventID
        var ev = this.Ets.Api.Data.DbEvent.Load.ByID(123).ThrowIfLoadFailed("Event ID", 123);
        
        // Assign values to the model object as needed
        ev.Capture01 = "Custom Value";
        ev.IsEdited = true;
        
        // Save and push the changes to the TrakSYS database
        this.Ets.Api.Data.DbEvent.Save.UpdateExisting(ev).ThrowIfFailed();
      }
      catch(Exception ex)
      {
        // Throw errors if the operation fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    
    
