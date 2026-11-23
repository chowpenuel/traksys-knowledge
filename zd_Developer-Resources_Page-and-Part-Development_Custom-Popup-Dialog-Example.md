# Custom Popup Dialog Example

*Source: https://portal.parsec-corp.com/hc/en-us/articles/12803897194643-Custom-Popup-Dialog-Example*
*Last updated: 2025-05-21T22:52:59Z*

---

Applies To | TrakSYS 10+

### **Summary**

Starting with TrakSYS 10, the primary web development paradigm shifted away from the heavy use of popups to the [Post-Redirect-Get](https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design) method of web development. However, there are still cases where the use of popups are needed according to the project requirements. There may also be a number of cases where using a popup may make more sense rather than redirecting to an entirely different page. For more simplistic popup requirements, several TrakSYS-specific JavaScript functions (such as [showDialog](https://docs.parsec-corp.com/tsweb/javascript-reference/ets/ui/showdialog), [alert](https://docs.parsec-corp.com/tsweb/javascript-reference/ets/ui/alert), and [confirm](https://docs.parsec-corp.com/tsweb/javascript-reference/ets/ui/confirm)) are available.

For more complex implementation requirements and scenarios, custom dialogs with several parts and additional functionality may be required. In these cases, it is possible to create custom dialog windows directly on a Page Definition with a combination of CSS classes and TrakSYS specific JavaScript calls. This article contains one possible way these types of popups can be created. Additional custom scripting can be added to further extend the functionality of the popup to meet implementation requirements as needed.

### **Example**

For the purpose of this example, a Visual Page Definition will be used to build the popup. However, other methods (such as custom Content Pages or Content Parts) can be used to provide the same functionality.

  1. In a Visual Page Definition, navigate to the Grid tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997043310099)  
  

  2. Select the current Row and add a new Row. This Row will contain the parts that are needed for the custom popup.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997058025363)  
  

  3. Select the newly created Row, and click the Edit Row button to access the Row properties.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997136681107)  
  

  4. In the CSS Class field, 2 classes are needed. The first class is the **hidden** class. This class will set the Row's display property to none, which will hide it on page load. This includes all of the parts included on this Row. The second class needs to be a unique CSS class to this Row. For the purpose of this example, "**myDialog** " is being used as the class name. This will help identify the Row when the popup is called from script.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997177852435)  
  

  5. After saving the changes, a part or method is needed to call the Row and display it as a visible popup. For the purpose of this example, a Buttons Part (`ETS.TsButtons`) was added to the first Row. To access the Click Actions of the button, click the ellipsis (`...`).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997208134419)  
  

  6. Within the On Client Click field, the following call is being used to bring up the popup on button click:  
  

         
         return ets.ui.showDialog($('.myDialog'), 'Confirm Changes')

The call uses the [showDialog](https://docs.parsec-corp.com/tsweb/javascript-reference/ets/ui/showdialog) method to display a popup. It references the Row's unique CSS class "myDialog" to display the Row as the contents for the popup.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997282158995)  
  

  7. After saving the changes, Parts can now be added to the second Row to be displayed in the popup. Under the Parts tab, 2 Forms Text Box Parts and 1 Buttons Part was added for this example.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997366397971)  
  

  8. Go into the properties of the second Buttons part (within the second row of the page).
  9. Click the ellipsis (`...`) to access the Click Actions of the Cancel button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997413680275)  
  

  10. Within the On Client Click field, enter the following code:  
  

         
         return ets.ui.closeDialog();
         

The call uses the [closeDialog()](https://docs.parsec-corp.com/tsweb/javascript-reference/ets/ui/closedialog) method to close the current popup window.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997446528915)  
  

  11. After saving the changes and previewing the page, only the button configured on the first row of the page renders on page load. All parts within the second row are hidden by default.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997476567315)  
  

  12. When the button is clicked, the popup appears as expected and displays all parts included on the hidden Row.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18997530678419)



From here, additional custom scripting can be written to interact with the elements contained within the popup.
