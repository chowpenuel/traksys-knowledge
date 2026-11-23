# Content Parts

## JobDetails

This part is designed to take a JobID, load the relevant information, and then visualize the results.

### Properties

#### Job ID

All data that will be visualized is related to the provided Order ID. The Order is loaded and validated before attempting any rendering. Most of the data is mapped from the `_viewBlocks_Orders_Job` view.

#### Header Text

If provided, this property defines the Text of the Header. If not provided, it defaults to "Order Details".

#### Show Header

When true, the Header is shown.

#### Target Values Key Prefix

The JobDetails part will load data relevant to the provided Order ID and will store that data in the Values Dictionary for parts to render. The provided Prefix is appended to all Value Keys used.

### Visualization

The part is visualized with a Header and then four Details Parts with a separator between each. These are shown conditionally based upon the type of Order and the available data. Main Details Displays the Name, State, Required material, Product, Material, and Recipe (for Batch Systems). Planned Details Displays the Planned Area, System, Quantity, Units, and Start Date Time. Actual Details If there is an Actual System value, it displays the actual Area, System, and Start Date Time. Notes Details If there are Notes, it displays the Notes.

### Script

Some aspects of this Part may be modified at the scripting level. These properties are intended to be configured once and typically do not require further changes. Data Type Formatting Specific formatting for Integer, Double, and DateTime values can be assigned as class level variables. When visualizing values, these formats are used. They have been assigned default values based on common implementation practice.

## Job Time Overview

This part serves as a visual time summary for the active Order on a given System. It expects a System ID to be provided through the values key `SystemID`.

The part loads the current Order for the System and presents its current progress, planned end, and projected end in minutes.

### Properties

There are no properties for this part.

### Visualization

The part consists of a Header and either a horizontal linear gauge or a message when no Order is running.

The Header displays `Order Time Summary`.

If an Order is running, the gauge displays the current Order time progress and includes markers for the following values:

#### Current Progress

The number of minutes since the Order started on the current System.

#### Planned End

The planned duration of the Order in minutes.

#### Projected End

The estimated end of the Order in minutes, based on the calculated estimated Job end time.

If no Order is running, the part displays the message `There is no Order running.`

### Script

The script controls the gauge calculation and display formatting.

The gauge maximum is rounded up to a nearby readable value based on the largest displayed time value. This rounding logic and the displayed minute formatting can be modified in the script if needed.
