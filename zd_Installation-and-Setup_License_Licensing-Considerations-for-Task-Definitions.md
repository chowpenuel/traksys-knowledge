# Licensing Considerations for Task Definitions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360051603654-Licensing-Considerations-for-Task-Definitions*
*Last updated: 2025-05-21T22:04:13Z*

---

Applies To | TrakSYS 10+

### Summary

This article explains the meaning of Task Definitions in TrakSYS as related to license-sizing decisions.

#### Task Definition

A Task Definition in TrakSYS represents a single production task and associated user-entered data for an instance of a System in the configuration. Task Definitions are commonly used to define electronic forms in TrakSYS along with the workflow rules for when the forms are to be completed. In the configuration below, the **Packaging 1** System is placed under **Packaging** Area.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360082857873)

This System has several different production tasks defined:

  * **Stage Materials  
  
**
  * **Prepare Forms  
  
**
  * **Hourly HACCP Check  
  
**
  * **Hourly Fill Weight Check  
  
**
  * **Bottle Inspection Check  
  
**
  * **Quality Control  
  
**
  * **Energy Shutdown**



This configuration represents seven (7) Task Definitions.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360082857913)  
  
If the configuration was made up of 10 similar Packaging Lines or Systems, then it would contain 10 x 7 = **70** Task Definitions. Note that Task Definitions configured under a Template Parent System do not count against license limits.

#### Task Definitions vs. Task Form Item Groups

When configuring Tasks in TrakSYS, the number of data points to be collected through user input are defined as Task Form Items. These Items are created in logical groupings known as Task Form Item Groups. A single group may represent all of the data elements of an electronic form to be associated with a Task Definition, or a section or subset of elements that may be used across multiple forms. Task Form Item Groups may be assigned to one or more Task Definitions. In the following Task Definition, the **Packaging HACCP** Task Form Item Group has been assigned to define the data to be collected for a Task Definition.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360082857973)  
  
The Task Form Item Group contains four (4) Task Form Items, where each Item represents a single data point to be input by a user.

![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360082858053)

The number of Task Form Items and Groups created in TrakSYS, and the number of references to Task Form Item Groups by Task Definitions, are **NOT** factors in counting for licensing purposes. For licensing purposes, the Task Definition count is equal to the total number defined under the Systems and Sub-Systems in the configuration.

#### Conclusion

When purchasing a TrakSYS license, the number of Task Definitions must be determined. To estimate the needed number of Task Definitions, consider the number of different production tasks that will be required for each System and/or Sub System, rather than the number of different electronic forms that will be defined to support these production tasks.
