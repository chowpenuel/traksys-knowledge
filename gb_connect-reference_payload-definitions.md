# Payload Definitions

In TrakSYS Connect, Payload Definitions describe the data and format being transported to/from TrakSYS. The following common types are supported, as well as the ability to create custom types.

* JSON
* XML
* CSV
* Query String
* String Only

## Key

When a Payload Definition is created, associated Classes and Methods are generated and named based on the Key specified in the configuration. By convention, Class and Method names should be camel cased (i.e. CamelCase).

{% hint style="warning" %}
When Payload Definitions are created, a full compile is necessary. The resulting Data Model Classes will be in the `ETS.Core.Scripting.TsConnect` namespace while corresponding methods will be in `api.Connect.Payloads`.
{% endhint %}

Special care should be taken if a Payload Definition Key is changed. A full re-compile will be necessary as well as updating any code that references the original Class and/or Method names. In addition, the names of any existing plug-in Classes will have to be updated to reflect the change in Key.

## Actions

### Import

For XML and JSON Payload Definitions, the configuration of Payload Field Definitions (i.e. the data fields the payload contains) can be significantly expedited via the Import Action for the Payload Definition Group. This option allows the user to import a sample file representative of the expected payload and have its selected fields automatically extracted and created in the configuration along with the the Payload Definition.

### View Model

The Data Model for a Payload Definition is comprised of one or more Classes and Properties created in `ETS.Core.Scripting.TsConnect` based on the Payload Field Definitions. The View Model Action will display an outline of the Class hierarchy that makes up the Data Model. This can serve as a reference when interacting with the Data Model in other scripting areas of the application.

### Create Script Class

This extensibility Action will create a plug-in Script Class that taps into certain points of the Transaction process (e.g. after the Data Model is created from the payload string, after the payload string is created from the Data Model). Once the script location is specified (e.g. Web, Logic, Module, Workflow), the Class will be generated and opened in the script editor.

{% hint style="warning" %}
The plug-in Script Class must be placed in the same area of the application where the corresponding payload will be transacted. Otherwise, the plug-in Class will not be called (e.g. if the payload is used in a Module, the plug-in Script Class should be placed in the Module group).
{% endhint %}

For a full description of this entity, see [Payload Definition](../entity-reference/configuration-entities/payload-definition).
