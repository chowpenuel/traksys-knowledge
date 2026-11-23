# Configuring and Using Script Class Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/16389539037459-Configuring-and-Using-Script-Class-Tags*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12+

### Summary

In TrakSYS 12, a new tag type called Script Class Tags was introduced. Similar to the original Script Tag type, they can be used to execute custom C# code to help process complex logic. However, the differences between the two tag types are in how the code is created and processed.

When a Script Tag is created, it creates a separate C# class for it and then creates an instance of the Tag. In a majority of instances, this should not create any issues. However, performance issues may occur if the installation contains a very large amount of Script Tags (e.g., thousands or tens of thousands of Script Tags in a single installation). In these scenarios, Script Class Tags can help to mitigate these performance impacts.

When a Script Class Tag is created, it references a single Script Class that is created within the TrakSYS configuration. Unlike the Script Class tag type, it does not create a separate C# class for every tag instance. Other tags and static parameters can be defined within the properties of the Script Class Tag, which can then be passed into and accessed by the referenced Script Class. This method can significantly reduce the initial Logic Service start times and help speed up each scan. Additionally, it provides a major benefit in C# code maintenance. If a change in code is needed for Script Tags, it will need to be applied to each tag individually. Since Script Class Tags reference a singular Script Class, then any changes to the Script Class will automatically apply to all Script Class Tags referencing that class. This is especially useful in scenarios where multiple tags contain the same scripting logic, but provide different parameters.

### Procedure and Example

#### Creating Tag Script Classes

Along with Script Class Tags, a new Logic Service Script Class type called Tag Script Classes was introduced. These Script Classes will contain the C# logic that will be executed by Script Class Tags. The following steps explain the standard procedure for adding an instance of a Tag Script Class. These steps assume that one or more Logic Service Script Groups have been created.

  1. In the TrakSYS Web, navigate to **Developer | Scripts | Logic**.
  2. In the first slice, select the desired Logic Service Script Group. Then, click the New button in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16558849413011)  
  

  3. In the New Script list, select the Tag Script Class option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16558928004115)  
  

  4. On the resulting page, provide a value for the Name field and click Save. For the purpose of this example "TagScriptClass" was used as the name.
  5. To access the code editor of the Script Class, click the newly created Tag Script Class on the second slice. Then, click the Script link on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16559252978195)  
  

  6. In the editor, note the class name as it will be used when configuring Script Class Tags.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16559279662227)  
  

  7. Repeat steps 2 through 4 to create additional Tag Script Classes as needed.



#### Creating Script Class Tags

The following steps explain the standard procedure for adding Script Class Tags. These steps assume that one or more Tag Groups have been configured.

  1. In the TrakSYS Web, navigate to **Configuration | Tags**.
  2. In the first slice, select the desired Tag Group. Then, click the New button in the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16562751673107)  
  

  3. In the New Tag list, select the Script Class Tag type.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16562787033107)  
  

  4. In the General tab of the Tag properties, provide a value for the Name field. Then, provide the class name of the Tag Script Class in the Script Class Name field. This will be the same value shown in step 6 of the previous section. For this example, "TagScriptClass" is being used. Finally, specify a Data Type for the tag. In this example, the String data type is being used.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16563192263315)  
  

  5. Next, navigate to the Evaluation tab. There will be properties to reference other tags in the installation (Source Tag ID 1 through 10) and properties that allow the user to define static values specifically for this Script Class Tag (Parameter 1 through 5). In this example, a Virtual Integer Tag has been assigned to Source Tag ID 1 and a value of 10 in the Parameter 1 field. Additional Source Tag ID and Parameter fields can be used as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16564196392595)  
  

  6. Click Save to save the changes.
  7. Repeat steps 2 through 6 to create additional Script Class Tags as needed.



#### Using Script Class Tags

The steps below provide a simple example of how referenced tags and defined parameters in Script Class Tags can interact with the referenced Tag Script Classes. These steps assume that the steps in the previous two sections have been performed. 

  1. In the TrakSYS Web, select the configured Tag Script Class and open the code editor.
  2. The following code was placed into the `EvaluateValue()` method of the Script Class. As the code comments suggest, it is retrieving the values from the Source Tag ID 1 and Parameter 1 fields specified in step 5 of the previous section. From there, it adds the two values together and returns a String value as a result to the Script Class Tag.  
  

         
         public override object EvaluateValue()
         {
           // Get the value of the referenced Virtual Integer Tag
           int tagValue = this.Source01Tag.ValueInteger;
           // Get the value of the defined Parameter
           int paramValue = this.Param01.AsInt();
           // Get the sum of the two values
           int valueTotal = tagValue + paramValue;
           // return the value to the Script Class Tag
           return tagValue + " + " + paramValue + " = " + valueTotal;
         }
         

  3. After saving the changes, start (or restart) the Logic Service to apply them.
  4. Using the built-in Tags page, users can now observe the tag value changes when it is triggered. In the image below, the Virtual Integer Tag has a value of 0. Therefore, the the final result is 10.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16565847641875)  
  
When the Virtual Integer Tag is changed to a different value, the Script Class Tag gets evaluated and executes the code within the Tag Script Class. The results are then returned to the Script Class Tag.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/16565905203475)


