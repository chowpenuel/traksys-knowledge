# Interface Transaction

## Summary

### Entity Name

Interface Transaction

### Database Table Name

`tInterfaceTransaction`

### API Object Name

`DbInterfaceTransaction`

### Entity Description

An Interface Transaction record represents an instance of data exchanged through a given Interface Definition.

## Properties

`InterfaceDefinitionID`

Specifies the parent Interface Defintion.

`ParentInterfaceTransactionID`

Specifies the parent Interface Transaction if multiple Transactions are performed.

`TransactionLink`

Connects this Transaction to another.

`CorrelationID`

Unique identifier used for asynchronous calls in scenarios where there is callback and a need to track a call through (likely a provided guid of some type).

`StartDateTime`

The Date and Time when the Interface Transaction started.

`EndDateTime`

The Date and Time when the Interface Transaction ended.

`ExpirationDateTime`

When the Interface Transaction entry expires and will be removed from the table.

`State`

The status of the Interface Transaction. Possible values are:

* **InProgress** = 0
* **Success** = 1
* **Failed** = 2

`StateDateTime`

The Date and Time when the most recent State value was updated.

`UserState`

An extensible field which is typically used to identify the current state of an Interface Transation. For example, a simple enumeration can be used.

`MessagePayload`

The raw content that was included within the Interface Transaction. The content depends on type that is used for the Payload (e.g., XML, JSON, CSV, etc.).

`ResponsePayload`

The raw content that was included within the response for the intial Interface Transaction call.

`EntityID`

The ID of the Entity (e.g. Job, Product).

`EntityKey`

The unique key of the Entity.
