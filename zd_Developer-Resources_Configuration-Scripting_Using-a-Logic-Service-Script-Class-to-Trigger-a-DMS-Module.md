# Using a Logic Service Script Class to Trigger a DMS Module

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360035503214-Using-a-Logic-Service-Script-Class-to-Trigger-a-DMS-Module*
*Last updated: 2025-05-21T23:11:14Z*

---

Applies To | TrakSYS 10+

### **Summary**

Data Management Service (DMS) is a logic execution engine designed to process longer running non-real-time business rules. Typical uses include pre-aggregation of data for improved report performance, and automated data transfers between TrakSYS and business systems.

DMS also supports the creation of script-based business rules that can execute longer operations without interfering with the real-time data capture being done by Logic Service. For example, a System Script Class can be implemented to trigger a DMS module execution at the end of every scheduled shift.

### **Procedure**

  1. In the Logic Scripts hub of the Developer section, create a new System Script class.
  2. Enter a name for the script class.
  3. Enter the script editor by clicking C# Script under Actions.
  4. Give the public class being edited a unique name (this will be the name used when assigning the script class to a specific system).
  5. In this example, the DMS module execution needs to be triggered at the end of every shift so the following sample code is added to the `PostScanShiftHistoryEnd` method of the script class:  
  

         
         //create dictionary instance if using args
         Dictionary<string, object> args = new Dictionary<string, object>();
         
         // Add module arguments here if needed
         args.Add("ShiftHistoryID", 2);
         args.Add("SystemID", 17);
         
         // convert args dictionary to string
         string argsString = context.Api.Util.General.ToArgsString(args);
         
         // instantiate module trigger model object
         var modTrigger = new ETS.Core.Api.Models.Data.DbModuleTrigger();
         
         // populate model object's properties
         modTrigger.TriggerDateTime = context.Now;
         modTrigger.TriggerKey = "DMS Module Trigger Key";
         modTrigger.Args = argsString;
         
         // insert into the module trigger table to execute and log any error
         var result = context.Api.Data.DbModuleTrigger.Save.InsertAsNew(modTrigger)  
                                                                  .ThrowIfFailed();
         

  6. Click Save & Close.
  7. In the Advanced tab of the parent system properties, enter the script class name that was used in step 4 into the Script Class Name field.
  8. Click Save.
  9. Restart Logic Service.



Now, at the end of every shift for the specified system, the sample code above will add an entry to the `tModuleTrigger` table with the necessary arguments for the DMS module to execute successfully (ShiftHistoryID and SystemID in this example).

Once the record is created, DMS will trigger the module with the corresponding key. The `tModuleTrigger` record is removed after it has been processed.
