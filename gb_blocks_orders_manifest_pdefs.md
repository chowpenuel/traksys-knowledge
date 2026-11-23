# Page Definitions

## Order Assign | Spoke

This page allows for the assignment of an Order to a specific System, Product, and (when appropriate) recipe combination.

### Information

This page lists the following properties for assignment:

#### System

Determined based up the Values Key SystemViewKey and the Order's Requested Material Code. The initial list of possible Systems is determined by finding the System View with a Key matching the SystemViewKey value. If the Order has a Requested Material Code, the list of possible Systems is further filtered by checking if each System can produce a Product that has a matching ProducedMaterial. The selected value will be assigned to the relevant tJobSystemPlanned.SystemID

#### Product

Determined based upon the selected System from the dropdown. The initial list of possible Products is determined by finding the Product Set for the selected System. If the Order has a Requested Material Code, the list of products is further filtered by checking if each Product produces the requested Material. The selected value will be assigned to the tJob.ProductID

#### Recipe

This is only visible for Batch JobTypes. The list of possible Recipes is determined based upon the selected Product. The selected value will be assigned to the tJobBatch.RecipeID

### Actions

The following actions are available:

#### Assign

Execute the update of the Order and relevant records.

## Order Edit Header | Spoke

This page allows for the editing of the core header information for an Order.

### Information

This page lists the following properties for editing:

#### Name

Provided by the user and assigned to the tJob.Name field.

#### State

Provided by the user and assigned to the tJob.UserState field. The value is based upon the Blocks.Orders.Enums.JobState Enum which is documented in the Scripts section.

#### Planned Production Group

Provided by the user and assigned to the tJob.Capture01 field. This value is used to determine which production group or view the Order appears under when it is not assigned to a specific System.

### Actions

The following actions lorem ipsum:

#### Save

Executes the update of the tJob record.

## Order Edit Notes | Spoke

This page allows for the editing of the Notes field of an Order

### Information

This page lists the following properties for editing:

#### Notes

Provided by the user and assigned to the tJob.Notes field.

### Actions

The following actions are available:

#### Save

Executes the update of the tJob record.

## Order Edit Planned | Spoke

This page allows for the editing of the planned production information for an Order.

### Information

This page lists the following properties for editing:

#### Start Date/Time

Provided by the user and assigned to the tJob.PlannedStartDateTime field.

#### Quantity

Provided by the user and assigned based upon the JobType. For Discrete Orders, the value is assigned to the tJobDiscrete.PlannedCalculationCount field. For Batch Orders, the value is assigned to the tJobBatch.PlannedBatchSize field. .

### Actions

The following actions are available:

#### Save

Executes the update of the tJob record.

## Order Edit Producing | Spoke

This page allows for the editing of the producing information for an Order.

### Information

This page lists the following properties for editing:

#### Requested Material

Provided by the user and assigned to the tJob.Capture02 field.

#### Product

Provided by the user and assigned to the tJob.ProductID field. The list of possible Products is determined based upon the Product Set of the planned System for the Order.

#### Recipe

This is only visible for Batch JobTypes. The list of possible Recipes is determined based upon the selected Product. The selected value is assigned to the tJobBatch.RecipeID field.

### Actions

The following actions are available:

#### Save

Executes the update of the tJob record.

## Order End | Spoke

This page allows for the ending of an active Order from a specific System.

### Information

This page lists the selected Order and its details.

### Actions

The following actions are available:

#### End

Attempt to End the Order on the current System. This validates the Order record using the standard TrakSYS Validation, the **Orders Block** extensible ValidateForEnd method, and validation that the Logic Service is running before attempting. It then executes the **Orders Block** extensible End method and then waits for the Logic Service to end all JobSystemActuals record for the Order before redirecting.

## Order | Hub 2

This page acts as a hub for viewing Order details and connecting to each category's respective Edit Page.

### Information

This page lists the following data:

#### Order

The main information for the order, including the Name, the State (according to the Blocks.Orders.Enum.JobState), and the JobType (if any).

#### Producing

The production master information, including the Product, the matching Material (if any) and the Recipe (for Batch Systems).

#### Planned

The main operational information, including the planned System, the planned Quantity and Units, and the planned Start Date Time.

#### Notes

A simple free-entry text field for notes and comments relating to the Order.

#### Bill of Materials

The listing of the total expected and planned quantities of relevant Materials based upon the configured Product. This is a comparison of the ProductMaterial and MaterialUsePlanned tables.

#### Planned Material

The listing of the total planned and actual quantities of relevant Materials based upon the execution of the Order. This is a comparison of the MaterialUsePlanned and MaterialUseActual tables.

#### Steps (Batch Systems only)

A listing of the expected BatchSteps with their operational sequence, name, and planned durations.

#### Parameters (Batch Systems only)

A listing of the related BatchParameters with their related sequence, name, and values.

### Actions

The following actions are available next to their related Headers:

#### Order - Edit

This action links to the Order Edit Header spoke. The JobID is taken from the Hub2's InstanceID.

#### Producing - Edit

This action links to the Order Edit Producing spoke. The JobID is taken from the Hub2's InstanceID.

#### Planned - Edit

This action links to the Order Edit Planned spoke. The JobID is taken from the Hub2's InstanceID.

#### Notes - Edit

This action links to the Order Edit Note spoke. The JobID is taken from the Hub2's InstanceID.

#### Planned Materials - Add Material

This action links to the Order Material New Edit spoke. The JobID is taken from the Hub2's InstanceID.

#### Planned Materials - Edit

This action links to the Order Edit Header spoke. The Material Use Planned ID is passed through the query string.

#### Planned Materials - Delete

This action prompts confirmation before attempting to delete the Material Use Planned record of the selected row.

## Order Material New Edit | Spoke

This page allows for the creation and editing of planned Material records for an Order.

### Information

This page lists the following properties for editing:

#### Material

Provided by the user and assigned to the tMaterialUsePlanned.MaterialID field. The list of possible Materials is determined based upon the Product's Bill of Materials, including any configured Material alternates. This value can only be changed when creating a new record. When editing an existing record, the Material is visible but cannot be changed.

#### Batch Step

This is only visible for Batch Orders. The list of possible Batch Steps is determined based upon the Function Definitions associated with the Batch. The selected value is assigned to the related Batch Step reference for the planned Material record.

#### Quantity

Provided by the user and assigned to the tMaterialUsePlanned.Quantity field.

#### Lot

Provided by the user and assigned to the tMaterialUsePlanned.Lot field.

### Actions

The following actions are available:

#### Save

Executes the creation or update of the tMaterialUsePlanned record.

## Order New | Spoke

This page creates Jobs for the current Production and System.

### Information

This page only allows for the input of a Name. Other fields and values are calculated.

#### Name

Provided by the user and assigned to the tJob.Name field.

#### OrderType

Determined based upon the Values Key SystemID. If no SystemID is present, it defaults to a Batch Order. Additionally, if a SystemID is present, a DbJobSystemPlanned record is created as well.

#### Production Group

Determined based up the Values Key SystemViewKey. It is expected to match a value from tSystemView.Key. The value is assigned to tJob.Capture01.

### Actions

The following actions are available:

#### Create

Executes the creation of the Order and relevant records.

## Order Reset | Spoke

This page allows for the reset of an Order.

### Information

This page lists the selected Order and its details.

### Actions

The following actions are available:

#### Reset

Resets key fields and records relating to the Order to allow it to be re-executed. This includes the removal of many child data records. This will reset the tJob.UserState field to Ready(1) and then delete all data records (and their children) that use the JobID as part of context: OeeInterval (Discrete-only), Batch (Batch-only), JobSystemActual, MaterialUseActual, Event, Task, Journal, SampleSubGroup, Transfer

## Order Start | Spoke

This page allows for the Start of an Order from a specific System.

### Information

This page lists the selected Order and its details.

### Actions

The following actions are available:

#### Start

Attempt to Start the Order on the current System. This validates the Order record using the standard TrakSYS Validation, the **Orders Block** extensible ValidateForStart method, and validation that the Logic Service is running before attempting. It then executes the **Orders Block** extensible Start method and then waits for the Logic Service to create a JobSystemActual record before redirecting.

## Order Unassign | Spoke

This page allows for the unassignment of an Order from a specific System.

### Information

This page lists the selected Order and its details.

### Actions

The following actions are available:

#### Unassign

Removes the ProductID from an Order, resets Capture01 to the current SystemViewKey in the values dictionary, and deletes any related JobSystemPlanned records. For Batching Systems and Orders, it also removes the RecipeID and deletes any related Batch records.

## Orders Assigned | Spoke

This page displays a list of Orders assigned to a System (by tJobSystemPlanned record).

### Information

This page lists the Orders in a table with the following columns:

#### Name

Taken from tJob.Name

#### Product

Taken from tProduct.Name and tProduct.ProductCode

#### Planned Quantity

Taken from tJobDiscrete.PlannedProductionCount or tJobBatch.PlannedBatchSize and their respective MeasureID fields, based upon Order type.

#### Planned Start

Taken from tJob.PlannedStartDateTime

#### State

The State is based upon the Blocks.Orders.Enums.JobState Enum which is documented in the Scripts section.

### Actions

The following actions are available for each Order in the table:

#### Details

This action links to the instanced Order Hub 1, passing the Order ID as the instance ID.

#### Start

This action only enabled for the first Order in the table, which is ordered by the PlannedStartDateTime of the Orders. It links to the JobStart Spoke, passing the Order ID in the query string.

#### Unassign

This action links to the Order Unassign Spoke, passing the Order ID in the query string.

#### Delete

This action prompts confirmation before deleting the Order record for the selected Row.

### Configuration

This page displays Orders that are assigned to the System (via the related tJobSystemPlanned.SystemID column for each tJob record) and the State is of the value 2 or lower. The State is based upon the Blocks.Order.Enums.JobState Enum. A value of 0 represents `New` and a value of 1 represents `Ready`.

## Orders | Hub 1

This page is a redirect page. It has no content and only acts as a Navigational Hub to redirect between the three Orders Spokes.

## Orders Past | Spoke

This page displays a list of the 20 most recent Orders that have been completed for a given System (has a tJobSystemActual record and UserState of 10 or higher).

### Information

This page lists the Orders in a table with the following columns:

#### Name

Taken from tJob.Name

#### Product

Taken from tProduct.Name and tProduct.ProductCode

#### Planned Quantity

Taken from tJobDiscrete.PlannedProductionCount or tJobBatch.PlannedBatchSize and their respective MeasureID fields, based upon Order type.

#### Planned Start

Taken from tJob.PlannedStartDateTime

#### Actual Start

Taken from tJobSystemActual.StartDateTime, based on the matching Order and System IDs. If multiple tJobSystemActual records exist, the Minimum Start Date Time is used.

#### Actual End

Taken from tJobSystemActual.EndDateTime, based on the matching Order and System IDs. If multiple tJobSystemActual records exist, the Maximum End Date Time is used. If a tJobSystemActual record with a NULL EndDateTime exists, the Order is active and the NULL is displayed.

#### State

The State is based upon the Blocks.Orders.Enums.JobState Enum which is documented in the Scripts section.

### Actions

The following actions are available for each Order in the table:

#### Details

This action links to the instanced Order Hub 1, passing the Order ID as the instance ID.

#### Reset

This action links to the Order Reset Spoke, passing the Order ID in the query string.

#### Delete

This action prompts confirmation before deleting the Order record for the selected Row.

### Configuration

This page displays Orders that have been completed on the given System (via tJobSystemActual) and with an appropriate UserState value. The UserState Enum is located under the Blocks Orders Shared Scripts, in the Order Enums script. Completed Orders are expected to have a UserState value of 10 or higher, which indicated a Complete or otherwise finished state.

## Orders Unassigned | Spoke

This page displays Orders that are assigned to the related production area but not to a specific system. See the configuration section below for more details.

### Information

This page lists Orders in a table with the following columns:

#### Name

Taken from tJob.Name

#### Requested Material

Taken from tJob.Capture02

#### Planned Quantity

Taken from tJobDiscrete.PlannedProductionCount or tJobBatch.PlannedBatchSize and their respective MeasureID fields, based upon Order type.

#### Planned Start

Taken from tJob.PlannedStartDateTime

#### State

The State is based upon the Blocks.Orders.Enums.JobState Enum which is documented in the Scripts section.

### Actions

The following actions lorem ipsum:

#### Details

This action links to the instanced Order Hub 1, passing the Order ID as the instance ID.

#### Assign

This action links to the Order Assign Spoke, passing the Order ID in the query string.

#### Delete

This action prompts confirmation before deleting the Order record for the selected Row.

### Configuration

This page displays Orders that are assigned to a production area via the tJob.Capture01 column and/or assigned to a System (via tJobSystemPlanned). When Orders are received from ERP or entered without an assigned System, they must contain an identifier in tJob.Capture01 that matches the value that this page is configured to filter for.

## Connect Orders | Hub 1

This page is a redirect page. It has no content and only acts as a Navigational Hub to redirect to the first accessible child page.
