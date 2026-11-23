# Configuring State Machines

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4415816319763-Configuring-State-Machines*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.2.2+

### **Summary**

In TrakSYS 11.2.2, State Machines were added. This feature provides a way to track the state of a specific entity (such as a Task, Job, Item, or Batch) on a Workflow diagram. Transitions between different states can be tracked and certain actions can be performed based on which transition takes place. This article outlines the prerequisites and configuration needed to use State Machines in Workflow diagrams.

**Note:** The Workflow Feature Line is required on the TrakSYS license in order to configure and use State Machines. 

### **Procedure**

#### **Configuring State Machines**

  1. Open the TrakSYS Web and navigate to **Developer | Workflow | State Machines**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665592135699)  
  

  2. Click the New button under the Groups section on the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665623587091)  
  

  3. Specify a Name and a Key for the group, then click the Save button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665658813587)  
  

  4. Select the newly created group and click the New button under the State Machines section on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665687162003)  
  

  5. Provide a value for the Name and Key fields. Then click the Save button to apply the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665755632659)  
  

  6. The State Machine should now appear within the list. Repeat steps 4 and 5 to add additional State Machines.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665772092435)  
  




#### **Configuring State Machine States**

State Machine States allow users to define custom enumeration values that represent various states. Workflow steps can be used to track these State values to identify the current State for an active Process.

  1. Select a State Machine on the second slice. Then click the States link under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665770277907)  
  

  2. On the resulting page, click the New button under the States section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665799326227)  
  

  3. Provide a value for the Name, Key, and Value fields. Then, click Save to save the changes. **Note** that the Value field only takes integer numbers.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665834665491)  
  

  4. Repeat steps 2 and 3 to create more States as needed. For the purposes of this example, 5 different States were created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665841637651)



#### **Configuring State Machine Transitions**

Transitions are defined to track changes from one State to another.

  1. Select a State Machine on the second slice. Then, click the Transitions link under the Related section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665854505363)  
  

  2. Next, click the New button under the Transitions section of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665899307027)  
  

  3. Provide a value for the Name field. Then, select a configured State Machine State for the From State Machine State and To State Machine State properties. Click the Save button to save the changes.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665903645075)  
  

  4. Repeat steps 2 and 3 to create additional Transitions as needed. For the purposes of this example 8 Transitions were created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665913995539)



#### **Configuring GetState and ChangeState Scripts**

GetState scripts are used to retrieve the current state for a given object (e.g., a Task, Job, Item, or Batch). The ChangeState scripts are used to execute code when a transition happens from one step to another. **Note** : Scripting in both of these areas is required in order to use State Machines in Workflow Diagrams.

  1. Select the State Machine and click the GetState Script link under the Actions section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20665973597331)  
  

  2. Insert script that will retrieve the value from the desired field. The example code used below retrieves the value from the `tJob.UserState` field. However, the code can be modified to retrieve values from other tables and fields as needed.  
  

         
         var job = (DbJob)model;
         if (job == null) return new Result<int>().AsError("Failed to load Job");
         return new Result<int>().AsSuccess(job.UserState);
         

  3. Click the Save & Close button after making changes to close the editor.
  4. Click the ChangeState Script link under the Actions section of the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20666000113427)  
  

  5. Custom code in this area will execute whenever a state change occurs. If no script needs to be executed on change, the line of code below can be inserted.  
  
`return new Result().AsSuccess(true);`  
  

  6. Click the Save button to save the changes.
  7. Click the Compile button to perform a Full Compile.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/20667722747667)  
  




At this point, State Machines can now be used in Workflow Diagrams and other scripting areas of the TrakSYS application. The Wait For State, Wait for State Change, and Set State Value Step Types can used to track and modify State values in a given Process. The TrakSYS API (e.g., the `Api.StateMachine` service) can be used to access and use State Machines in custom code as needed.
