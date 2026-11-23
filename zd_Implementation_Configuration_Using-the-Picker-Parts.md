# Using the Picker Parts

*Source: https://portal.parsec-corp.com/hc/en-us/articles/13096733675923-Using-the-Picker-Parts*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.2.0+

### **Summary**

Picker Parts can be used to give a visually appealing way of selecting values on a page. The Pickers provide a list of pregenerated options that can help minimize issues in value selection. The range of available Picker parts allow the selection of built-in entities as well as values selected from a custom SQL query (depending on which Picker Part is used).

When using the Picker Parts, a minimum of two Parts are required per Picker:

  * The Forms Picker Input Part (`ETS.Forms.TsInputPickerInput`)
  * The Picker Part that will display the desired data (such as the Icon Picker Part (`ETS.Pickers.TsPickerIcon`)).



The Forms Picker Input Part will provide the initial Picker button. The second Picker Part will provide the list of clickable options when the initial button is clicked. This article provides an example of how to use the Forms Picker Input Part with other Picker Parts.

### **Procedure**

  1. On a new Visual Page Definition, go into the page properties and click the Grid tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775747033619)  
  

  2. Add columns to the existing row to help separate the Parts. As mentioned in the [Interface Design Best Practices](https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design), typical column widths are 2, 8, and 2, but can vary depending on specific needs and implementation requirements. In the example below, a fixed column of 160 pixels has been created for the first column. It is then followed by columns with widths of 9 and 3. The final result is shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/32285141553043)  
  

  3. Next, navigate to the Parts tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775827811731)  
  

  4. In the middle column, add a Picker Input Part (`ETS.Forms.TsInputPickerInput`).
  5. In the third column, add a Picker Part under the "Pickers" section to display contents. For the purpose of this example, an Icon Picker Part (`ETS.Pickers.TsPickerIcon`) was selected.  
  
The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775966297107)  
  

  6. Go into the properties of the Picker Input Part. Specify a value for the Form Key and the Picker Key.  
  

     * The **Form Key** will provide the selected value and can be referenced in code or by other parts to retrieve the value.
     * The **Picker Key** will contain the value that will link the Picker Input Part with other Picker Parts on the page. The Picker Input and other Picker Part **must** contain identical Picker Keys so that the selectable options can be displayed when the picker button is clicked.
For the purpose of this example, a Form Key of "Form.Icon" and a Picker Key of "Picker.Icon" was specified.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19775997784723)  
  

  7. After saving the changes, go into the properties of the other Picker Part (e.g., the Icon Picker Part for this example). Under the General tab, provide the identical value for the Picker Key field. For this example, it is the "Picker.Icon" value specified in the previous step.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19776052972307)  
  

  8. After saving the changes, click the Preview button to view the page.
  9. The page should display the default, blue picker button. Click the button to bring up the contents of the Icon Picker Part. The final results should be similar to what's shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19776181024019)  
  

  10. Once an Icon has been assigned, the CSS class name for the icon will be displayed in the Picker Input Part.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/19776253981843)  
  
The value can now be referenced through the Form Key using custom scripting or from within other Content Parts.


