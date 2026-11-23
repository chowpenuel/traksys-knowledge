# System Discrete Real-Time Overview

The System Discrete Real-Time Overview page displays real-time data for the specified Discrete System.

{% hint style="warning" %}
**Manual Events**

In order for this region to function properly, the System for which this Page is displaying data must have manual Event Definitions configured with virtual Trigger Tags.

**Display Units**

Note that the produced units shown on the Production Progress Bar are the Display Units configured on the System's KPI Calculation (under the Advanced tab). Meanwhile, the units shown under the Planned Quantity of the Job are the Planned Production Count Units set on the Job record.
{% endhint %}

## General

### Name

Identifies the page throughout the application. If either Navigation Title or Page Title are provided, the Page Title will be used in their respective place.

### Key

Used to reference the page programmatically and within the URL. Each Page Key must be unique within each hierarchy.

### Icon

Displays an icon in the title of the page.

### Navigation Icon

Displays an icon in the navigation to the page.

### Navigation Title

This Title is used on links to this page from the Tree View and elsewhere. If no value is provided, the Page Name is used in its place.

### Page Title

This Title is displayed at the top of the very top of the page. If no value is provided, the Page Name is used in its place.

### Refresh Keys

Used to refresh the page remotely either by Logic Service or any time the Keys are called, typically by a System or Tag configured with Refresh Keys (see the Configuration Section for more information). Multiple Keys can be used in this field by separating with a comma.

### Refresh (Minutes)

Sets a fixed page refresh every X minutes, independent of the Refresh Keys configured. The default is 0 minutes, meaning that no scheduled refresh will occur.

### Preview URL

Specifies the URL that will be used when the page is Previewed. If no value is specified, then the default page URL will be used.

### Instance Type

Specifies the type of Instancing that will be used for the page. This property can be defined directly on page creation, but will display as ready only after the page has been created. At this point, the Instance Type can be changed for the individual page within the Developer Section.

### Page Level Type

This read-only field displays whether the page is a Section, Hub 1, Hub 2, Hub 3, or Spoke.

### Content Key

This read-only field displays the Content Key which can be referenced when linking to this type of page directly. For example, using `C={ContentKey}` in the URL will link directly to the desired Content Page without having to instance the page.

## Visibility

### Header Visible

Option to show or hide the standard blue TrakSYS header at the very top of the page. The Inherit option uses the same selection from the page above in the hierarchy.

### Footer Visible

Option to show or hide the standard blue TrakSYS footer at the very bottom of the page. The Inherit option uses the same selection from the page above in the hierarchy.

### Title Visible

Option to show or hide the Page Title at the top of the page. The Inherit option uses the same selection from the page above in the hierarchy.

### Breadcrumbs Visible

Option to show or hide the Breadcrumbs, or trail of pages at the top of the page. The Inherit option uses the same selection from the page above in the hierarchy.

### Tree Visible

Option to show or hide the Tree on the left side of the page. The Inherit option uses the same selection from the page above in the hierarchy.

### Spokes Visible

Option to show or hide the links to the Spokes on this level of the hierarchy on the top right of the page. The Inherit option uses the same selection from the page above in the hierarchy.

### Visible in Navigation

Option to show or hide links to this page in the Header, Tree, or Spokes Navigation. The Inherit option uses the same selection from the page above in the hierarchy.

## Back

### Back Visible

Option to show or hide the Back button on the top right side of the page.&#x20;

{% hint style="info" %}
To display the Back button, the Spokes Visible property also must be set to True (or Inherit if the page above it is set to True). If Spokes are hidden for the page, then the Back button will not be shown even if the Back Visible property is set to True
{% endhint %}

### Back Button Caption

Specifies the Caption that is displayed on the Back button. If no value is provided the button will display "Back" for the button text.

### Back Icon

Specifies the Icon that will be displayed on the Back button. If no Icon is selected the "fa-circle-left" Icon will be displayed automatically.

### Return URLs Excluded

Specifies the list of URLs that should be excluded when the user clicks the Back button. Multiple URLs can be included in this list with one URL per line.&#x20;

## Properties

### System

Specifies the System ID for which to display data.

### KPI Calculation

Specifies the OEE Calculation ID for which to display data.

### System Data Mode

Determines whether this Page will be focused on displaying more Shift oriented data or Job oriented data.

### Behavior | Allow Active Events

Determines whether active Events can be acknowledged. Default value is No.

### Column Widths

**Left** - Determines the width (1-12) of the left column of the page, typically where filters or details are displayed.

**Center** - Determines the width (1-12) of the center column of the page, typically where tabular data or charts are displayed.

**Right** - Determines the width (1-12) of the right column of the page, typically where selected data information is displayed.

**Tile** - Specifies the width (1-12) of any Tiles displayed on this Page.

**Chart** - Specifies the width (1-12) of any Charts displayed on this Page.

## Content

### Task Top N

Determines the maximum number of Tasks to be displayed on this Page.

### Journal Top N

Determines the maximum number of Journal entries to be displayed on this Page.

### Allow | Job Details

Determines whether or not to display the Job Details region of this Page.

### Allow | Shift History Details

Determines whether or not to display the Shift region of this Page.

### Allow | Manual Events

Determines whether or not to display the Manual Events region of this Page.

### Allow | Tasks

Determines whether or not to display the Tasks region of this Page.

### Allow | Journal

Determines whether or not to display the Journal region of this Page.

## Links

The following properties allow for the specification of link targets when clicking various elements on the Page. Any URL within the TrakSYS application (or external) can be specified. In some cases, QueryString parameters may be passed to the target using Values Keys that are available on this Page. Some link properties include a default URL that directs to a standard Page when the value is left empty (these defaults are specified below when applicable).

### Job Overview

Specifies an alternate link to the Job Overview Page. If this value is blank, the default link is:

`?c=ETS.Application.Job.JobDiscreteOverview&JobID={JobID}&SystemID={SystemID}`

### Job End

Specifies an alternate link to the Job End Page. If this value is blank, the default link is:

`?c=ETS.Application.Job.JobDiscreteEnd&JobID={JobID}&SystemID={SystemID}`

### Job Planned

Specifies an alternate link to the Job Planned Page. If this value is blank, the default link is:

`?c=ETS.Application.Job.JobDiscreteListForSystemPlanned&SystemID={SystemID}`

### Shift History Overview

Specifies an alternate link to the Shift History Overview Page. If this value is blank, the default link is:

`?c=ETS.Application.Shift.ShiftDiscreteOverview&ShiftHistoryID={ShiftHistoryID}&SystemID={SystemID}`

### Event Active

Specifies an extensible link to an Event Active Page. There is no default link at the current time. Values Keys that can be used in the link include:

* `c=ETS.Application.Event.EventAttention`
* {Data.ActiveEvent.ID}
* {SystemID}
* {JobID}

### Event Attention

Specifies an alternate link to the Event Attention Page. If this value is blank, the default link is:

`?c=ETS.Application.Event.EventListAttention&Systems={SystemID}`

### Task Overview

Specifies an alternate link to the Task Overview Page. If this value is blank, the default link is:

`?c=ETS.Application.Tsk.TaskOverview&SystemID={SystemID}`

### Task New

Specifies an extensible link to Task New Page. There is no default link at the current time. Values Keys that can be used in the link include:

* `c=ETS.Application.Tsk.TaskNewEdit`
* {SystemID}

### Task Edit

Specifies an alternate link to the Task Edit Page. If this value is blank, the default link is:

`?c=ETS.Application.Tsk.TaskNewEdit&TaskID={TaskID}`

### Journal Overview

Specifies an alternate link to the Journal Overview Page. If this value is blank, the default link is:

`?c=ETS.Application.Journal.JournalOverview&SystemID={SystemID}`

### Journal New

Specifies an alternate link to the Journal New Page. If this value is blank, the default link is:

`?c=ETS.Application.Journal.JournalNewEdit&SystemID={SystemID}`

### Journal View

Specifies an alternate link to the Journal View Page. If this value is blank, the default link is:

`?c=ETS.Application.Journal.JournalView&JournalID={JournalID}`

### Show | Job Overview

Determines whether or not to enable the link when clicking the Overview button at the top of the Job Details region of this Page.

### Show | Job End

Determines whether or not to enable the link when clicking the End button at the top of the Job Details region of this Page.

### Show | Job Planned

Determines whether or not to enable the link when clicking the Planned button at the top of the Job Details region of this Page.

### Show | Shift History Overview

Determines whether or not to enable the link when clicking the Overview button at the top of the Shift Details region of this Page.

### Show | Event Active

Determines whether or not to enable the link to a custom Page when clicking the Event Active Tile. Note: the Event Active Tile will only become interactive when a link value is specified for Event Active.

### Show | Event Attention

Determines whether or not to enable the link when clicking the Acknowledge Tile in the Events region of this Page.

### Show | Task Overview

Determines whether or not to enable the link when clicking the Overview button in the Tasks region of this Page.

### Show | Task New

Determines whether or not to enable the link to Task New Page when clicking the New button in the Tasks region of this Page. Note: this button will only become interactive when a link value is specified for Task New.

### Show | Task Edit

Determines whether or not to enable the link when clicking a Task row in the Tasks region of this Page.

### Show | Journal Overview

Determines whether or not to enable the link when clicking the Overview button in the Journal region of this Page.

### Show | Journal New

Determines whether or not to enable the link when clicking the New button in the Journal region of this Page.

### Show | Journal View

Determines whether or not to enable the link when clicking a Journal row in the Journal region of this Page.

## Charts

### Production Width

Specifies the width (in pixels) of the Production progress bar.

### Production Height

Specifies the height (in pixels) of the Production progress bar.

### Event Width

Specifies the width (in pixels) of the Event charts displayed on this Page.

### Event Height

Specifies the height (in pixels) of the Event charts displayed on this Page.

### Event Top N

Specifies the number of rows/columns to display in each of the Event charts displayed on this Page.

### Show | Production Progress

Determines whether or not to display the Production progress bar.

### Show | Production State

Determines whether or not to display the Production state chart.

### Show | Events by Sub-System

Determines whether or not to display the Events by Sub-System chart.

### Show | Events by Definition

Determines whether or not to display the Events by Definition chart.

### Show | Events by Category

Determines whether or not to display the Events by Category chart.

## Advanced

### Format | Product

Determines how Product information, if any, will be formatted on the page. The "Name Only" or "Code Only" will show either the Product Name or the Product Code, respectively. The "Name and Code" option will show the Product Name with the Product Code in brackets (e.g. ProductName \[ ProductCode ] ). Conversely, the "Code and Name" option will display the Product Code with the Product Name in brackets. This format can be set using the Values Key `Theme.FormatProduct` and passing in a valid enum value.

### Format | Date/Time

Determines how Date/Time information, if any, will be formatted on the page. See the [Number and Date Format](../../../../expression-syntax/format/number-and-date-format) topic. This format can be set using the Values Key "Theme.FormatDateTime" and passing in a valid Date/Time format.

### Format | Date

Determines how Dates, if any, will be formatted on the page. See the [Number and Date Format](../../../../expression-syntax/format/number-and-date-format) topic. This format can be set using the Values Key "Theme.FormatDate" and passing in a valid Date format.

### Format | Quantity

Determines how quantities, if any, will be formatted on the page. See the [Number and Date Format](../../../../expression-syntax/format/number-and-date-format) topic. This format can be set using the Values Key "Theme.FormatQuantity" and passing in a valid Number format.

### Format | Tile

Determines how a Tile, if any, will be displayed on the page. This format can be set using the Values Key "Theme.FormatTile" and passing in a valid enum value.

### URL | Success URL

This field determines where the Page will redirect upon successful execution. If no value is provided, the Return URL is used.

### URL | Return URL

This field determines where the Page will redirect if the User decides to cancel execution and go back to a previous Page. If no value is provided, the user will be returned to the Page from which they came.

## Notes

### Alternate Name

Similar to the Alternate Name property on Configuration entities, this field is another name to reference the page by. This field can only be seen by those with access to edit the properties of the page.

### Description

Provides an area for documenting a textual description or purpose of a page. This field can only be seen by those with access to edit the properties of the page.

### Notes

Provides an area for providing key details and notes about a page. This field can only be seen by those with access to edit the properties of the page.
