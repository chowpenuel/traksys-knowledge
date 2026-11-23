# Interface Definition

## Summary

### Entity Name

Interface Definition

### Database Table Name

`tInterfaceDefinition`

### API Object Name

`DbInterfacedefintion`

### Entity Description

An Interface Definition specifies the data transport mechanism for TrakSYS Connect (i.e. how a Payload will be sent or received).

## Properties

`Interface Definition Group [ InterfaceDefinitionGroupID ]`

Specifies the parent ID of the related Interface Definition Group.

`Linked Interface Definition [ LinkedInterfaceDefinitionID ]`

The ID of the associated Interface Definition.

`InterfaceType [ InterfaceType ] : ETS.Core.Enums.InterfaceDefinitionType`

Specifies how the Interface Definition will process transactions. Possible values are:

* **Custom** = 0
* **WebServiceCall** = 1
* **WebServiceEndpoint** = 3
* **FilePush** = 5
* **FilePull** = 6

`Message Payload Definition [ MessagePayloadDefinitionID ]`

The ID of the associated Payload Definition. This is the message that will be used for the initial Interface Transaction call.

`Response Payload Definition [ ResponsePayloadDefinitionID ]`

The ID of the associated Payload Definition. This is the message that will be used for the response as a result of the initial Interface Transaction call.

`ModuleTriggerKey [ ModuleTriggerKey ]`

The Module Trigger Key that will be called when a call is made to the Interface Definition.

`ProcessDefinitionKey [ ProcessDefinitionKey ]`

The Workflow Process Definition Key that will be called when a call is made to the Interface Definition.

`CompleteTransactionOnSuccess [ CompleteTransactionOnSuccess ]`

Enabled by default, Transaction is automatically marked as complete when finished. It can be disabled for additional customization, allowing for handling and completion of an Interface Transaction in a post method.

`EntityIDType [ EntityIDType ]`

Type of the EntityID (e.g. Job, Product).

`ContentParameters [ ContentParameters ]`

The parameters that will be included when a call is made to the Interface Definition.

`ExpirationHours [ ExpirationHours ]`

Determines how long Interface Transactions are kept.

`SavePayloadToTransaction [ SavePayloadToTransaction ]`

Determines if Payload is saved to the Transaction record.

`Correlation Header Key [ ContentParameters ] : Web Service Endpoint Only`

Specifies a value for a request header key and is used to track requests across a system. When a value is provided, the Endpoint will attempt to read this key from the request headers and add it to the Interface Transaction. This value is stored as part of a JSON string in the `ContentParameters` field.

`File Service Name [ ContentParameters ] : File Push and File Pull Only`

This property provides the option to specify a namespace for custom implementations of the `IConnectFileService`. This value is stored as part of a JSON string in the `ContentParameters` field.

`HTTP Client Type Name [ ContentParameters ] : Web Service Call Only`

This property provides the option to specify a namespace for custom implementations of the `IConnectHttpClient`. This value is stored as part of a JSON string in the `ContentParameters` field.

`Content Parameters [ ContentParameters ] : Custom Only`

This property specifies additional properties and configuration for the Interface Definition. The content is usually provided in JSON format.
