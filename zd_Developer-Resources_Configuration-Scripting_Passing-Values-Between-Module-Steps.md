# Passing Values Between Module Steps

*Source: https://portal.parsec-corp.com/hc/en-us/articles/15025026590227-Passing-Values-Between-Module-Steps*
*Last updated: 2025-05-21T23:10:07Z*

---

Applies To | TrakSYS 10+

### **Summary**

A Module may contain multiple Module Steps that represent distinct operations to run in sequential order. There are several different types of Module Steps that can be configured for a parent Module. Module Script Steps can pass arguments to the next Module Step for different purposes. This is useful for determining if certain conditional logic should execute based on certain values. This method can also be used to determine whether the next Module Script Step should be executed. This article contains a simple example for both of these scenarios.

### **Examples**

#### **Passing Values Between Module Steps**

This example shows how multiple values of different data types can be passed between different Module Script Steps.

  1. Access the TrakSYS Web and navigate to **Developer | Modules**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18882689746451)  
  

  2. Click the New button in the first slice to create a new Module.
  3. Within the Module properties, provide a Name and set the Trigger Mode to None. Then set a value for the Trigger Key. If TrakSYS 11.2.1 or older is being used, specify computer name of the machine that hosts the Data Management Service in the Host field. If TrakSYS 11.2.2 or newer is being used, choose a Data Management Service Instance under the Module Manager setting (as shown below).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18882722957587)  
  

  4. Click the Save button to apply the changes.
  5. Select the newly created Module on the first slice. Then, click the New button on the second slice.
  6. Within the list of Module Steps, choose the Script Module Step option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18882729405971)  
  

  7. Provide a Name for the Module Script Step and click Save.
  8. The following code was added into the `Execute()` method of the script. As shown, 3 different variables with different variable types were declared. Each variable is then added to the `Args` to be passed into the next Module Step.  
  

         
         public override bool Execute(IModuleContext ctx)
         {
           // Declare local variables.
           int argsValue1 = 10;
           string argsValue2 = "String Value";
           bool argsValue3 = true;
         
           // Add the values to the Args to be passed into the next step.
           ctx.Args.Add("Param1", argsValue1);
           ctx.Args.Add("Param2", argsValue2);
           ctx.Args.Add("Param3", argsValue3);
           return true;
         }
         

  9. Click the Save & Close button on the script editor.
  10. Repeat steps 5 through 7 to create a second Module Script Step.
  11. The following code was added into the `Execute()` method of the script. As shown, the 3 variables are retrieved from the `Args` and placed into local variables. Then, the TrakSYS API is being used to create a log entry in tLogCustom, which contains all three of the values.  
  

         
         public override bool Execute(IModuleContext ctx)
         {
           // Retreive the values from the Args.
           int param1 = ctx.Args.GetAsInt("Param1");
           string param2 = ctx.Args.GetAsString("Param2");
           bool param3 = ctx.Args.GetAsBool("Param3", false);
         
           // Create a log entry in tLogCustom to output the values.
           ctx.Api.Util.LogCustom.WriteInformation("Param 1 = " + param1 + 
                                                   " Param2 = " + param2 + 
                                                   " Param3 = " + param3, 
                                                   "Param Arguments", "");
           return true;
         }
         

  12. Click the Save & Close button on the script editor.
  13. Start (or restart) the Data Management Service.
  14. Navigate to **Administration | Services | Data Management**. Locate the newly created Module within the Modules list and click the Execute button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18882838197267)  
  

  15. After successfully executing the Module, query the tLogCustom table. The `tLogCustom.Message` field should contain the parameter values.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15122960100883)



#### **Determining if the Next Module Script Step Will Be Executed**

This example shows how the next Module Script Step can be executed or skipped based on a value passed into the `Args` from the previous step. The example continues from the steps outlined in the previous example.

  1. Access the script editor of the first Module Script Step and change the value of the `argsValue1` variable to 1. The final code example should now look similar to the following:  
  

         
         public override bool Execute(IModuleContext ctx)
         {
           // Declare local variables
           int **argsValue1 = 1;**
           string argsValue2 = "String Value";
           bool argsValue3 = true;
         
           // Add the values to the Args to be passed into the next step
           ctx.Args.Add("Param1", argsValue1);
           ctx.Args.Add("Param2", argsValue2);
           ctx.Args.Add("Param3", argsValue3);
           return true;
         }

  2. Click the Save & Close button on the script editor.
  3. Within the Modules configuration page, select the second Module Step on the second slice. Then, click the Edit button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18882876874515)  
  

  4. Place the following text into the Execute when True property of the step:  
  

         
         {args|Param1}

  
![](https://portal.parsec-corp.com/hc/article_attachments/18882918050067)  
  
This property specifies a TrakSYS expression which should return 1 or 0. If the expression returns 1, the Module Step will execute. Otherwise, if the expression returns 0, the Module Step will not execute and will be skipped. The value used for this property uses the `args` expression syntax to reference the `Param1` key present in the `Args` (which was passed in from the first Module Script Step).
  5. Click Save to apply the changes.
  6. Start (or restart) the Data Management Service.
  7. Navigate to **Administration | Services | Data Management** and manually execute the Module.
  8. When querying the tLogCustom table, the entry should appear and display the Args values in the Message field.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/15125980590867)



To prevent the Module from executing a value of 0 will need to be provided. To demonstrate this, repeat step 1 and change the `argsValue1` variable to 0. Then, repeat steps 6 though 8 to view the results. In this scenario, when the tLogCustom table is queried, there should **not** be an additional entry as the second Module Step should have been skipped.
