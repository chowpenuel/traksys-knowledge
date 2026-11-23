# Custom Task Visualization

*Source: https://portal.parsec-corp.com/hc/en-us/articles/8133230124947-Custom-Task-Visualization*
*Last updated: 2024-07-24T18:27:15Z*

---

### **Introduction**

This article provides Page Definitions of a Frequently Requested Example (FRE). The pages provided are intended to provide a starting point for Developers who are looking to use more complex Development Tools. This is intended to augment the existing Training Information and Reference Documentation, but is not intended to be implemented directly into a production environment. 

Attached to this article is a zipped folder that contains one or more Page Definitions. The intended way to implement these pages as well as a short description of the capability they are meant to display are listed below. Additional information about the use and purpose of the Page Definitions is included on the Pages and can be viewed once they have been imported.

### **Capability**

These pages show an example of using the AddCustomTaskItemContentParts method to control the rendering of TaskItems done by the TsInputTaskItems part. 

There are two examples provided:

  * Page Script - This shows a simpler example where all logic is contained on the Script of the Page. 
  * Web Script - This shows a more complex example, where all logic is refactored to a Web Script Class that contains more dynamic logic and the Page Script can use simplified calls to achieve the same result. This example contains multiple execution examples in a single page and be more difficult to follow.



### **Page Deployment**

The following represents the intended deployment pattern of the attached Page Definitions. It represents the Hierarchy by using a Bulleted List and the Keys from the Page Definition files.

  * Custom Task Visual 
    * PageScript
    * WebScript



#### **Additional Components**

There is a "GenericVisualizer.txt" script that is intended to be implemented as a Web Script Class. To do this, navigate to the "Developer" Section of the implementation, select the "Scripts" Hub 1, then the "Web" Hub 2. Create or select a Web Script Group. Create a new Web Script and open the Script Editor and replace the entire contents with the provided script. Be sure to compile the script before attempting to use the WebScript page.

The Web Script example also requires specific Task Form Items for some of the visualizations to function as intended. The expected Task Form Items are listed below. The Task Form Item Group and Task Definition configuration does not require specific configuration.

**Name** | **Key** | **DataType**  
---|---|---  
First and Last Name | FirstAndLast | String  
Timestamp | DateTime_Timestamp | String  
Pick an Event Code | DropDown_EventCode | Integer  
Ready for Sign-Off | ReadySignOff | Discrete  
  
  
Lastly, the "Pick an Event Code" Task Form Item requires a SQL statement to be provided in the "Notes" field. 
    
    
    SELECT ID [Value], [Name] [DisplayName] FROM tEventCode

Alternative Task Form Items can be used to trigger any of the other defined logical elements in the Web Script. Read the Web Script to determine what other options are readily available.

#### **Revisions**

27th July 2022 - Initial Publication (v11.2.3)

Contact the [Parsec Applications Department](mailto:applications@parsec-corp.com) for any questions, comments, or concerns.
