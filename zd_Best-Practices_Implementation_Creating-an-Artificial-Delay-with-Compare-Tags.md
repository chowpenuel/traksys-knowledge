# Creating an Artificial Delay with Compare Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/42122035029395-Creating-an-Artificial-Delay-with-Compare-Tags*
*Last updated: 2025-06-30T22:07:26Z*

---

Applies To | All Versions

### Summary

In some cases, a delay may be required to slow down detected Tag value changes. This is typically common in scenarios where rapid tag value changes for Trigger Tags cause unintended production data. For example, if a Tag changes values too quickly when it is assigned as a Trigger Tag to an Event Definition or Task Definition, this may unintentionally create too many Event or Task records. This issue is commonly caused by environment-specific issues such as faulty PLC's that occasionally send bad values or connectivity issues that interfere with receiving Tag values at the correct times. To help mitigate these issues, the Compare Tag has a True Delay property that can be used to create an artificial delay. This can be useful to help verify whether Tag value changes are legitimate and can prevent extra records from being created due to unintended value changes.

**Note:** The caveat to this method is that it can create lost time in some instances. For example, if this technique is used for Trigger Tags on Event Definitions and the value set for the delay is set to 10 seconds, the first 10 seconds of an Event will never be recorded (even if the tag value change is legitimate). 

### Procedure

The following steps demonstrate how the Compare Tag's True Delay property can be used to create an artificial delay. These instructions assume that the original Tags already exist within the TrakSYS installation. It also assumes that the original Tag contains a Discrete data type. However, other data types can be used as needed.

  1. In the TrakSYS Web, navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42122035005715)  

  2. Select the desired Tag Group on the first slice. Then, click the New button on the second slice.
  3. Within the list of Tag options, click the Compare Tag entry.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42122035009555)  

  4. Provide a name and Data Type for the Tag. For the purpose of this example, a Discrete Data Type has been selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42122023997331)  

  5. Within the available options, the Compare Tag has the Left Operand, Operation, and Right Operand settings. These settings help determine the conditions that will be evaluated when determining whether the Compare Tag should change values. For the Left and Right Operand fields, either a static value or a Tag can be assigned for the evaluation process. In this example, an OPC UA Tag has been assigned to the Left Operand and a value of 1 was assigned to the Right Operand. With these settings, the Compare Tag will watch the OPC UA Tag and begin the evaluation process when that Tag contains a value of 1.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42122023999763)  

  6. Next, navigate to the Delay tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42122035017875)  

  7. Within the list of options, the True Delay (Seconds) setting will be present. This is the delay (in seconds) before the Compare Tag value changes once the expression evaluates to True. In the example below, a value of 10 seconds has been specified. This means that once the conditions for the expression configured in step 5 have been met, the Compare Tag will wait 10 seconds before changing values. If the condition is still met after the delay, then the Compare Tag will change value. Otherwise, if the condition is no longer met within the 10 second time period, then the Compare Tag will retain the current value.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42122024010003)  

  8. Finally, navigate to the Value tab.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/42125752909075)  

  9. Within the list of options, the Tag Value if Compare is True setting will be present. This is the value that will be returned when the full conditions of the Compare Tag and Delay are met. In the example below, the Compare Tag will return a value of 1 when the conditions are met  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42125709194131)  
  
Alternatively, a different Tag can be referenced to return that value instead. As an example, if the original OPC UA Tag value should be returned, that Tag can be assigned to this property.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42125752914451)  

  10. Finally, save the changes and start (or restart) the Logic Service.



If the Compare Tags are being used to create delays for Trigger Tags under System Definitions (such as Event or Task Definitions), the Compare Tag itself should be assigned as the Trigger Tag instead of the original Tag. Once all Tags have been reassigned, the Logic Service will need to be restarted as these are considered configuration changes.
