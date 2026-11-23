# Interface Definitions

In TrakSYS Connect, Interface Definitions describe the how the data payload is transported to/from TrakSYS. The following common types are supported, as well as the ability to create custom types.

* Web Service Endpoint (hosted in TrakSYS, called by external systems)
* Web Service Call (hosted externally, called by TrakSYS)
* File Pull
* File Push

## Key

When an Interface Definition is created, associated Classes and Methods are generated and named based on the Key specified in the configuration. By convention, Class and Method names should be camel cased (i.e. CamelCase).

{% hint style="warning" %}
When Interface Definitions are created, a full compile is necessary. The corresponding methods will be in `api.Connect.Interfaces`.
{% endhint %}

Special care should be taken if an Interface Definition Key is changed. A full re-compile will be necessary as well as updating any code that references the original Method names. In addition, the names of any existing plug-in Classes will have to be updated to reflect the change in Key.

## Actions

### Create Script Class

This extensibility Action will create a plug-in Script Class that taps into certain points of the Transaction process (e.g. after incoming payload is received and converted to the Model). Once the script location is specified (e.g. Web, Logic, Module, Workflow), the Class will be generated and opened in the script editor.

{% hint style="warning" %}
The plug-in Script Class must be placed in the same area of the application where the corresponding Interface will be used. Otherwise, the plug-in Class will not be called (e.g. if the Interface is used in the Web, the plug-in Script Class should be placed in the Web group).
{% endhint %}

For a full description of this entity, see [Interface Definition](../entity-reference/configuration-entities/interface-definition).
