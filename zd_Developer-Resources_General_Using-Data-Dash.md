# Using Data-Dash

*Source: https://portal.parsec-corp.com/hc/en-us/articles/33627225508115-Using-Data-Dash*
*Last updated: 2025-05-21T22:49:38Z*

---

Applies To | TrakSYS 10.2.5+

### Summary

When building pages, it may be desirable to access values through client-side JavaScript code when data is displayed in various controls. The Data-Dash functionality provides a way to help create additional HTML elements on a per-row basis. This allows users to write client-side code that interacts with these values to provide additional functionality. The following built-in Parts have access to Data-Dash functionality:

  * List View
  * List View Markdown
  * Table View
  * Data-Driven Tiles (Dynamic Width)
  * Data-Driven Tiles (Fixed Width)
  * Div (TrakSYS 11.0.0+)



### Example

This example uses a Table View Part to demonstrate the Data-Dash functionality. Similar steps can be used for all other Parts that have access to this feature.

  1. Access the TrakSYS Web and create a new Visual Page Definition (under **Developer | Page Definitions**).
  2. Within the Parts tab of the Page, add the Table View (`ETS.Lists.TsTable`) and Custom SQL Data Table (`ETS.DataTables.TsDataTableCustomSql`) Parts.
  3. In the Properties of the Custom SQL Data Table Part, enter a query that will retrieve data from the Table View Part. For this example, the query shown below is being used to provide Event-related data to the table.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33702227914003)  
  

  4. Provide a value for the Target Values Key setting under the Data tab. For this example, "`Data.Events`" is being used as the Key. Then, click Save to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33702227920659)  
  

  5. In the properties of the Table View Part, define the values for the Caption and Content fields. For this example, the following values are being used:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33703757374611)  
  

  6. In the Data tab, enter the value that was provided for the Target Values Key in Step 4.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33703757376531)  
  

  7. Finally, navigate to the Data-Dash tab. Enter a Key and Value for the fields that should be exposed to client-side code. The value for the **Key** will be used when the field is exposed in the HTML. This can be any value, but it is recommended to use a value that accurately represents the data being exposed. The **Value** field should reference the column in the query that should be exposed. TrakSYS Expressions can be used to reference this column.  
  
In the example below, only a single row (EventID) has been specified. It is possible to specify multiple rows as needed. Doing so will expose multiple values per data row for the Part.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33703757380243)  
  

  8. Click Save to apply all changes.
  9. Preview the page. A table of Events should be displayed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33703793247123)  
  

  10. Press F12 to bring up the browser Developer Tools. The DOM Selector can be used to select individual rows for inspection. The screenshot below shows this option while using the Google Chrome browser. The location of this option may be slightly different depending on the browser.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33703793253395)  
  

  11. Within the HTML of the Part, the Data-Dash key is shown with the applicable value. When this key is generated, it will have the following format:  
  

         
         data-{Key}
         

The Key is the key value specified for the column in Step 7. Since the Key was defined as "EventID" in this example, the full Data-Dash key is `data-eventid`. The screenshot below shows the exposed key-value pair for the first three rows of data. Notice that each of these values match the values returned for the EventID column on each row (as shown in Step 9).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33703937815315)  
  
Now that the key-value pair has been exposed for each row, it can be properly referenced in client-side JavaScript code as needed.


