# Using Task Form Item Conditionals

*Source: https://portal.parsec-corp.com/hc/en-us/articles/48443764434195-Using-Task-Form-Item-Conditionals*
*Last updated: 2026-03-03T01:10:56Z*

---

### Introduction

TrakSYS 14 introduced new properties on Task Form Items to support conditional logic within Tasks. This enhancement allows Task Items to be dynamically shown or hidden based on evaluated conditions.

This article introduces the new functionality and covers the following:

  * Core functionality and behavior
  * A technical overview of the conditional syntax
  * An example with simple and nested conditional statements
  * Recommended best practices and considerations



### Core Functionality

Both Task Form Items and Task Items have been updated to support conditional logic through the following new fields:

**TaskFormItem** :

  * IsConditional (Boolean)
  * Condition (String)



**TaskItem** :

  * IsHidden (Boolean)



The**IsConditional** property on a TaskFormItem determines whether conditional logic applies. This value defaults to False, ensuring existing and upgraded environments are not impacted unless explicitly configured. When set to True, the associated Condition expression is enabled. Any TaskItems created from a conditional TaskFormItem are initialized with IsHidden = True.

When rendering a Task using the built-in TaskItems Content Part, TaskItems with the IsHidden property set to True are omitted from the User Interface (UI). These items still exist within the TaskData object and the Database which means they remain accessible for processing or inspection. However, they will not displayed to the end user. Even if a hidden TaskItem’s condition would evaluate to true based on default values, it will not be processed or displayed until the Task is saved for the first time.

To support this behavior, the TaskService introduces a new method called **ProcessConditionals**. This method is automatically invoked as part of all TaskData save operations, but it can also be called independently when needed.

ProcessConditionals iterates through the TaskItems in a TaskData instance and re-evaluates each item’s conditional logic:

  * If a TaskItem meets its condition, IsHidden is set to False.
  * If a TaskItem no longer meets its condition, IsHidden is set to True, and its value is reset to the default value defined on the TaskFormItem.



On subsequent renders, the Task reflects the updated visibility state of each TaskItem based on the evaluated conditions.

### Technical Overview

Conditional logic for Task Form Items is implemented using the **Dynamic Expresso** expression interpreter. This framework allows simple, single-line conditional expressions to be defined directly in configuration, without requiring a full scripting environment.

Expressions are written using a C#-like syntax and are evaluated at runtime to determine whether a TaskItem should be shown or hidden. These expressions **only evaluate values** and cannot declare variables, assign values, or perform multi-line logic. Each expression must resolve to a boolean result.

Conditional expressions can reference other Task Items within the same Task. During the ProcessConditionals API call, Task Item values are exposed to the expression engine as read-only keys. These keys are generated using the related Task Form Item Group key and Task Form Item key in the following format:
    
    
    TaskFormItemGroupKey_TaskFormItemKey

Each key maps to the current value of its corresponding Task Item, allowing Task Items to be conditionally evaluated based on the values of other Task Items within the Task.

### Example

The following example assumes the following configuration is being used:

  * Task Form Item Group
    * Name: Inspection
    * Key: Inspection



#### Task Form Items

  * **Has Defect**
    * Key: HasDefect
    * Data Type: Boolean (Yes / No)
    * IsConditional: False
  * **Defect Reason**
    * Key: DefectReason
    * Data Type: String (LookupSet)
    * Options: None, Scratch, Crack, Discoloration, Other
    * IsConditional: True
    * Condition: Inspection_HasDefect == true
  * **Defect Count**
    * Key: DefectCount
    * Data Type: Integer
    * IsConditional: True
    * Condition: Inspection_HasDefect == true
  * **Defect Description**
    * Key: DefectDescription
    * Data Type: Text
    * IsConditional: True
    * Condition: Inspection_HasDefect == true && Inspection_DefectReason == "Other"



This configuration demonstrates a simple, chained set of conditional Task Form Items.

When the Task is first rendered, only **Has Defect** is displayed because it is not conditional. If Has Defect is set to True, the conditions for **Defect Reason** and **Defect Count** are fulfilled and both fields become visible. If Defect Reason is then set to Other, the condition for **Defect Description** is also fulfilled and the text field appears.

If Has Defect is later set back to False, none of the conditional items meet their criteria. As a result, Defect Reason, Defect Count, and Defect Description are all hidden again, and their values are reset to their respective default values.

The examples above focuses on simple equality-based conditions, but conditional expressions can vary based on the underlying data type. 

For example, the following expressions are also valid:

  * A Boolean value can be used directly as a condition:


    
    
    Inspection_HasDefect

  * A string value can reference its length:


    
    
    Inspection_DefectDescription.Length > 20

  * Numeric values can be evaluated using basic mathematical expressions:


    
    
    Inspection_DefectCount / 10 >= 0

While the expression engine supports additional variations, not all constructs are available in this constrained environment. During configuration, conditional expressions are validated when saved. If an expression cannot be evaluated correctly, an error will be displayed, indicating the issue and allowing the condition to be corrected.

### Best Practices

While conditionals allow for more dynamic and flexible Task Forms, it is important to remain within the intended scope of a Task. Tasks are designed to represent individual forms. Although it is possible to place a large amount of content into a single Task, it is recommended to split complex workflows into multiple Task Forms and trigger follow-up Tasks as needed. These Tasks can still be related using ParentTaskID or similar patterns, while avoiding overly complex or difficult-to-maintain conditional logic.

When nested conditionals are required, always include **all preceding conditions** in the expression. This helps ensure predictable evaluation and avoids unexpected visibility changes caused by processing order. For example, the **Defect Description** field includes both the _Has Defect_ and _Defect Reason_ checks, rather than relying solely on the dropdown value.

With the addition of conditional visibility, it is expected that end users may interact with a Task multiple times before completing it. To maintain clarity and traceability, the following is recommended:

  * Use the TaskItem’s CompletedDateTime and User fields to track individual inputs.
  * Use the Task’s UserState to identify Tasks at different stages of the workflow.



Following these practices helps keep Task configurations maintainable, predictable, and easier to support over time.
