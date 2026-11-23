# Licensing Considerations for Event Definitions and Tags

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360051604094-Licensing-Considerations-for-Event-Definitions-and-Tags*
*Last updated: 2025-05-21T22:03:57Z*

---

Applies To | TrakSYS 10+

### Summary

This article explains the difference between Tags and Event Definitions in the TrakSYS environment. The purpose is to clarify decision-making when considering the appropriate license size for an implementation.

#### Tags

A Tag in TrakSYS represents a single data point or variable. Tags are typically thought of as data points from automation systems (PLCs and HMIs). These are called OPC Tags in TrakSYS, but there are also several other types of Tags that can be defined. Values can be brought in from relational data sources (Database Tags) or calculated using a number of programmatic type Tags (Compare, Boolean, Switch, etc…).

TrakSYS also contains specialized Tag types called Script Tags that allow a nearly unlimited amount of logic to be defined in .NET languages to calculate a single value. Business rules and configuration are created in the TrakSYS environment by combining the real-time input type Tags (typically OPC) together with the logic type Tags (Compare, Boolean, Switch, Script, etc…).

The following tree diagram is an example of how several Tags can be used to define a trigger for recording an event. **Note:** this type of diagram is for illustration purposes and does not appear on any configuration screens.

![](https://portal.parsec-corp.com/hc/en-us/article_attachments/210752348/Tree.PNG)

The items in the above tree each represent a Tag. The BL1.FILLER.MOTOR_RUNNING and BL1.FILLER.TEMP are examples of OPC Tags coming from control systems. The BL1.FILLER.TEMP_HIGH Tag (Compare Tag) defines a comparison between the filler temperature Tag and a constant value of 96. The result of this comparison becomes another Tag value that can be used in further Tag definitions. The final Tag, BL1.FILLER.OVERHEATED (Boolean Tag) executes a Boolean AND operation on the temperature high condition and the actual motor running status from the control system.

Regardless of the size of the License, TrakSYS does not limit the number of Tags that can be configured.

#### Event Definitions

The Event Definition entity is a key element to TrakSYS configuration and its license model. An Event Definition is a single, automatically detectable reason that a System can experience an event. The events recorded by an Event Definition can represent any type of machine state (down, slow, starved, waiting, running, etc…), but are typically used to signify fault or error conditions. Note that Event Definitions configured under a Template Parent System do not count against license limits.  
  
Event Definitions are the primary mechanism by which event analysis is viewed for Systems. The chart below is a typical example of an event report for a System grouped by Event Definition.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360084057573)

The following is an example of a filling production line Sub-System configuration.

The Filler Sub-System is configured with five Event Definitions that represent different fault states that will be automatically monitored and recorded as they occur.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360084064053)  
  
In addition to machine driven Event Definitions, Systems are typically configured with event conditions that are controlled by human interaction. The image below shows an example of manual events configured for a packaging line. Even though the conditions that drive these events are typically activated manually, TrakSYS considers these real-time inputs and Event Definitions are used to specify the trigger logic.  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/360084066853)  
  
The trigger condition for an Event Definition is defined as a single discrete (1 or 0 / On or Off) Tag value. In both of the above images, the Tag that controls the triggering of the Event Definition is shown below the Event Definition Name in Slice 2 (the Event Definitions Slice).  
  
In some cases the trigger Tag for an Event Definition can be a single discrete data point (Tag) coming from the control system. In other cases, the trigger Tag is the culmination of many Tags (as in the Filler Overheated Event Definition and Tag shown in the example above).

### Conclusion

In addition to Event Definition triggers, Tags are also used for many other parts of the TrakSYS configuration. There are typically many more Tags used in the configuration than the number of Event Definitions.  
  
The TrakSYS license size is based primarily on the number of Event Definitions that are allowed to be configured. Estimating how many automated event reasons (Event Definitions) each System in the implementation will require is important in selecting the correct size for the TrakSYS License.
