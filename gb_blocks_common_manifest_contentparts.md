# Content Parts

## System Overview

This part provides an overview for a given System, including links to further detail, an overview of the current Job, and an overview of common Metrics.

### Properties

#### System ID and System Key

The part first attempts to load by ID, if not null, before loading by Key.

A System is required because all rendered data is based on the System.

#### Navigation URL

This controls where the Tile and Menu Links redirect to.

If no URL is provided, the links are disabled.

### Visualization

This part renders a Header, Menu, and four data segments.

If the System has no active Job, only the Header, Menu, and first segment render.

#### Header and Menu

These identify the System name and provide a link to the System.

By default, this link is blank and needs to be configured.

#### Segment 1 - Current Order

If a job is running, this identifies the Job's Name, expected Product, and expected Quantity.

If no Job is running, this identifies that no Order is running.

#### Segment 2 - Current Order Progress

This displays the current progress of the Order.

For a Discrete Job, this includes the Unit count produced and remaining Units, as well as a projection of time remaining.

For Batch Jobs, it identifies the current Step information, the next step, and a similar projection of time remaining.

#### Segment 3 - Order Metric

For Discrete Systems, this identifies the OEE for the current Order.

For Batch Systems, it identifies the Job's progress and three additional metrics: Adherence, Variance, and On-Time for the current Order.

#### Segment 4 - Day Metric

This provides the same metrics as Segment 3, but for the current Day instead of the current Order.

### Script

The metrics in the segments are calculated as part of the part.

For Discrete Systems, this pulls from `viewOeeInterval`.

For Batch Systems, this pulls from the `tBatchStep` table.

Alternative metrics can be defined and mapped to various segments.

This type of adjustment would likely require a rebuild of the individual segments, but can follow the existing structure.

## Logic Service Details

This part is designed to provide a live status indicator for a given Logic Service.

By default, it hides itself if Logic Service is running and only displays if Logic Service is offline or experiencing an issue.

This provides a way to indicate to operations and end-users if Logic Service is down and, as a result, visualizations or data may appear incorrect.

It appears with a green circle if it is running, a red circle if it is stopped, and an orange circle for any other state.

### Properties

#### Host and Instance

These properties identify which Logic Service should be checked.

It finds the first Logic Service for the current Site where the Host and Instance information matches.

If neither property is set, they are ignored and the first Logic Service for the Site is used instead.

#### Show Details

If true, the part also renders a Details part that contains the Name, Host, and State of the associated Logic Service.

#### Hide if Running

When true, this part hides itself when Logic Service is in a running state.

#### Message if Running/Not Running

When not provided, the part renders a message alongside the color indicator for the Logic Service.

The message defaults to the Name of the Logic Service Host being rendered.

These properties can be used to conditionally override the message.

### Visualization

If Show Details is true, this renders a Header and Details part, listing the Name, Host, and State of the associated Logic Service, including the colored circle.

If Show Details is false, this renders only the colored circle and State message of the associated Logic Service.

If Hide if Running is true, this hides entirely when running and only displays when the associated Logic Service has a different state.

## Systems Overview

This part acts as a repeater, wrapping around the **System Overview** part.

It has minimal unique logic and relies on the **System Overview** part.

### Properties

#### System View Key

This part attempts to load a System View using the provided key.

It then iterates over the System View to create a **System Overview** part for each System within the View.

#### Navigate URL

This property identifies where the Tile and Menu Links for each Overview should go.

By default, it uses the current Page Key and sets the System's Key as the instance key.

### Visualization

This part has no specialized visualization.

It creates an instance of the **System Overview** part for each System within a new column with no additional logic.

The new column is set to have a Card for visual aesthetic.

### Script

Most of the logic is in the **System Overview** part and should be changed there.

If needed, the logic to determine how the System list is obtained can be adjusted, or minor adjustments to how the new Columns and rendering are encapsulated can be employed.

## Shift History Details

This part is designed to take a ShiftHistoryID, load the relevant Shift History information, and visualize the results.

### Properties

#### Shift History ID

All data that will be visualized is related to the provided Shift History ID.

The Shift History is loaded first, then the related Shift and Team are loaded when available.

#### Header Text

If provided, this property defines the Text of the Header.

If not provided, it defaults to `Shift Details`.

#### Show Header

When true, the Header is shown.

#### Target Values Key Prefix

The ShiftHistoryDetails part loads data relevant to the provided Shift History ID and stores that data in the Values Dictionary for parts to render.

The provided Prefix is appended to all Value Keys used.

### Visualization

The part is visualized with a Header and a Details part.

If no Shift History is found, a `No Current Shift` message is shown.

#### Details

Displays the Shift, Team, Start Date Time, and End Date Time when available.
