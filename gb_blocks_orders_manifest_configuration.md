# Configuration

## Database Views

This Function Block includes views based on the prefix `_viewBlocks_Orders_`.

### \_viewBlocks\_Orders\_Job

This view provides high-level information about the Order, including its planned and actual execution. The data is sourced primarily from the tJob, tSystem, tArea, and tProduct tables.

### \_viewBlocks\_Orders\_JobBatchStepPlanned

This view provides Batch Step records, filtered to include only Expected steps, and joined with tFunctionDefinition to expose the appropriate step name.

### \_viewBlocks\_Orders\_JobBom

This view provides Product Material data, joined with the Material and Measure tables to add contextual information.

### \_viewBlocks\_Orders\_JobMaterialActual

This view aggregates planned and expected Material Use values for comparison. It presents both sets of values along with contextual names, units of measure, and related information.

### \_viewBlocks\_Orders\_JobMaterialPlanned

This view provides individual Material Use Planned records, joined with the Function Definition, Material, and Measure tables to provide additional context.

## Interface Definitions

The Interface Definitions are used to configure inbound and outbound integration points for the **Orders Block**.

Inbound web service endpoints use a configured route value, but the full endpoint URL is based on the server and API path where the Block is installed. For example, when the configured route is `orders`, the resulting endpoint may look like:

`<server url>/TS/api/<site>/connect/<route>`

When configuring an inbound Interface Definition, use the **Copy Endpoint URL** property to retrieve the full endpoint URL for the current environment.

### Materials (External to TS)

This is an inbound web service endpoint for receiving Materials from an external system.

The configured route is `materials`.

### Order Status (TS to External)

This is an outbound web service call for sending Order Status information to an external system.

This interface is configured as a placeholder and should be updated with the appropriate target URL and authentication settings before use.

### Orders (External to TS)

This is an inbound web service endpoint for receiving Orders from an external system.

The configured route is `orders`.

## Notification Definitions

The Notification Definitions are used in the Manage pages of the **Common Block** as part of the Messaging pages and capabilities. They provide additional hooks for common actions related to Orders. The descriptions below focus on the expected triggers. For additional details on the Messaging functionality, refer to the **Common Block** documentation.

The Notification Definition’s Key is mapped to a constant in the Orders Message script. Any changes to these Notification Definitions, or any new Notification Definitions, need to be reflected in the Orders Message script as well.

The Notification Definition’s Description is used to store the Placeholders that can be used as tokens when building a Message. It expects a line-separated list, with each element containing a two-part, comma-separated value.

General:

`PlaceholderPrefix,NameSpace.ContainingClass+NestedClass`

Included format:

`Order,Blocks.Orders.OrdersMessageService+MessageOrder`\
`Urls,Blocks.Orders.OrdersMessageService+MessageUrls`

The Notification Definition’s Notes can be used to store any filter values that should be applied before sending.

### Batch Order End

Triggered when a Batch Order is ended.

### Batch Order Start

Triggered when a Batch Order is started.

### Discrete Order End

Triggered when a Discrete Order is ended.

### Discrete Order Start

Triggered when a Discrete Order is started.

## Payload Definitions

The Payload Definitions are used for **Orders Block** interface messaging.

All Payload Definitions use JSON payloads. These definitions are placeholders and do not have configured child elements or field mappings.

### Materials

This payload is used by the Materials web service endpoint.

It is configured as a JSON payload placeholder.

### Order Status

This payload is used by the Order Status web service call.

It is configured as a JSON payload placeholder.

### Orders

This payload is used by the Orders web service endpoint.

It is configured as a JSON payload placeholder.

## Permission Sets | Orders

These permissions are configured for general use across the Block.

### Permission Items

#### Manager

This permission is not directly referenced.

#### Supervisor

This permission is commonly referenced to control if certain actions are enabled.

#### User

This permission is not directly referenced.
