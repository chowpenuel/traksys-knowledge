# Using Linked Systems

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360009367593-Using-Linked-Systems*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 10+

### **Summary**

The following provides an explanation with an example of Linked Systems / SubSystems and how they can be used to relate concurrent Events from a SubSystem and System together in the TrakSYS database. The example will provide instructions for using this feature when adding configuration to the TrakSYS Web, as well as how to view Linked Event data using standard Content Pages. Users of this article should have prior experience modeling production processes in the TrakSYS Web using Areas, Systems, SubSystems, and Event Definitions.

### **Explanation**

Linked Systems allow the Logic Service to associate Events from a SubSystem with Events from a different System that occur at the same time. This feature is typically used when it is required to report Events for an Equipment Center two ways:

  * As part of a Production Line or Process, where the Equipment Center is modeled as a SubSystem to the Production Line’s System.
  * As an independent System, where Events associated with the Equipment Center do not get “masked” or hidden by simultaneous Events from other equipment on the Line.



In this scenario, you would need to duplicate the total number of Event Definitions for the Equipment Center in the configuration (for both the SubSystem on the Line and for the equipment’s independent System) to have the same level of detail reported in both views. This may not be a viable modeling approach due to the TrakSYS licensing limits for Event Definitions, particularly in large configurations. Linked Systems eliminates the need to duplicate Event Definitions by configuring all of the detailed events beneath the equipment’s System and linking to these from its corresponding SubSystem.

### **Example**

Consider a Production Line with 3 Equipment Centers. For this example, the Production Line will be referred to as the “Parent System” and the Equipment Centers as the “Child Systems”. In the configuration, each Equipment Center will be modeled as both a System and as a SubSystem to the Production Line. Faults and alarms will be configured for each Equipment Center beneath its corresponding System. The screenshots shown below show the Area and System Configuration.

#### **Configured Area and Systems:**

![](https://portal.parsec-corp.com/hc/article_attachments/18759879006099)

#### **Parent System SubSystems:**

![](https://portal.parsec-corp.com/hc/article_attachments/18759887067923)

The following Event Definitions have been configured for Child System 1:

![](https://portal.parsec-corp.com/hc/article_attachments/18760110555155)

The Child System will be configured as a SubSystem to the Parent, linking each one to their corresponding System. A single Event Definition will also be created beneath each SubSystem that will represent a general purpose Event. The Event Definition shown below has been configured for each Child SubSystem:

![](https://portal.parsec-corp.com/hc/article_attachments/18760191132691)

Within the properties of the SubSystems, the Linked System property has been set to reference each corresponding System.

![](https://portal.parsec-corp.com/hc/article_attachments/18760257801875)

The General Fault for the Child SubSystem will be triggered whenever any of the Event Definitions are active on the Linked System. This ensures that the Child SubSystem triggers an Event (the General Fault) for each active Event on the Child System (the Named Faults). In the example below, a Boolean Tag has been configured as the trigger tag for the Fault Event Definition for the Child SubSystem. It will return a value of 1 (to trigger the event) if any of the Event Definitions are triggered from the corresponding Linked Child Systems.

#### **Boolean Tag Properties:**

![](https://portal.parsec-corp.com/hc/article_attachments/18760556116627)

#### **Boolean Tag Operands:**

![](https://portal.parsec-corp.com/hc/article_attachments/18760629825555)

Using this configuration, the Logic Service will link the general Events for the Parent System with the detailed Events from the independent Child Systems. Think of this as another attribute of the Parent System's Events, similar to an assigned Event Category or OEE Type. Using the Event Overview Page (**ETS.Application.Event.EventOverview**) in the TrakSYS Web, you can group Event data by **Linked Event Definition with System** , allowing you to report by the detailed Event (the Named Faults) rather than by the general one.

![](https://portal.parsec-corp.com/hc/article_attachments/18760758623251)
