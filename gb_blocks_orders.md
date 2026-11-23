# Orders

## Overview

The **Orders Block** contains user interfaces, business logic, and capabilities for creating, viewing and managing the core attributes of production Orders (TrakSYS Jobs).

## Capabilities

The following sections describe the various capability use-cases provided by this Block.

### Create Orders directly in TrakSYS

The Orders Block includes all the necessary pages and parts ready to create orders (TrakSYS Jobs) directly in TrakSYS.

### Manage System Order Assignments (Assign, Unassign, Reset)

This Block contains multiple pages to allow users to manage order assingments to specific Systems, whether the orders were created in TrakSYS or not; so long as they haven't been started yet. Orders that may have been imported from ERP without a system assignment must be assigned to a System before they can be started.

### View and Manage Order Details

This Block includes parts and pages to visualize Order details throughout various production and administrative areas.

### Manage Order Materials and Planned Production Details

The Block also contains sets of pages to manage Order Materials (Bill of Materials) and Planned Production details such as specifying lots and quantities of input materials and planned quantities of production output. Alternatively, these details may be imported from an ERP system but still viewed and edited (if permissible) in TrakSYS.

### Review Orders across Production Areas and Systems

This Block allows users to view all orders, of varying states, throughout Production Areas and Systems modeled in TrakSYS. The base navigation established enables many of the other capabilties discussed here (i.e. assign, start, complete, reset, etc.).

### Start, Monitor, and Complete an Order

This Block sets up a standard approach for Orders to be started, completed, and reset. The Block also contains content parts to make it simpler to visualize real-time Order telemetry including durations and quantities against plans.

## Dependencies

### License

This section lists dependencies for TrakSYS Features required by this Block.

#### Discrete Jobs

Discrete Job functionality is available to any TrakSYS license starting with Bronze bundles.

#### Batch Jobs

Batch Job functionality requires Function Definitions, available starting in Gold bundles.

### Blocks

This section lists other Blocks that must be used for this Block to function.

#### BLOCKS.COMMON

The Orders Block must be deployed alongside the Common Block.

### Configuration

This section lists configuration assumptions used throughout this Block.

#### Table `tJob` | Field `Capture01`

This field holds a string identifier that signifies a production area or subset of Systems that can produce this Order. It is used to identify where this Order should be displayed before being assigned to a System (or when it is unassigned from a System). See the Orders Page Definition for usage.
