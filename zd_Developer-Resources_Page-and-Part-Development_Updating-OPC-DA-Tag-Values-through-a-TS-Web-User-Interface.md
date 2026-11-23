# Updating OPC DA Tag Values through a TS Web User Interface

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115002864073-Updating-OPC-DA-Tag-Values-through-a-TS-Web-User-Interface*
*Last updated: 2025-05-21T22:53:27Z*

---

Applies to | TrakSYS 10+

### **Summary**

OPC Tag values cannot be updated directly from the TS Web, these changes must be relayed through the Logic Service.

This can be done by updating a Virtual Tag and having the Logic Service compare this new value with the OPC Tag value. If they are different, the Logic Service updates the OPC Tag value with the new Virtual Tag value. 

### **Procedure**

The following example shows how to update an OPC Tag value from a user interface:

  1. Navigate to **Configuration | Tags**.
  2. For the OPC Tag in question (e.g. Name: TestTag.Opc), create a corresponding Virtual Tag (e.g. Name: TestTag.Virtual). Please note that the Virtual Tag and the OPC Tag need to have matching data types. The String data type will be used in this example.
  3. Create a Script Tag (e.g. Name: TestTag.Script). In this example, the Script Tag returns a Boolean. Alternatively, a Script Class may be used. 
  4. Select the newly created Script Tag and click the Script button under the Actions section in the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998283075091)  
  

  5. Add the script below to compare the OPC and Virtual Tag values. If the values are not the same, the OpcWriteback() method updates the OPC Tag value with the Virtual Tag value.  
  

         
         // retrieve the current tag values
         var virtualTagValue = Tags["TestTag.Virtual"].ValueString;
         var opcTagValue = Tags["TestTag.Opc"].ValueString;
         
         // Compare the Tag values
         if (virtualTagValue != opcTagValue)
         {
           // Copy the Virtual Tag value to the OPC Tag using OpcWriteBack
           this.Context.OpcWriteBack("TestTag.Opc", virtualTagValue);
           return 1;
         }
         return 0;
         

  6. Restart the Logic Service.



When viewing the tags in the Administration section's Tags page after restarting the Logic Service, the OPC and Virtual Tags will have the same default value initially:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998396254099)

Clicking Edit Value for the Virtual Tag and updating its value will also update the OPC tag. Updating the Virtual Tag value from a page definition will have the same result.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998383458707)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18998428483475)
