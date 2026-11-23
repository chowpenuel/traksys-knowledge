# Discrete Job Overview

The Discrete Job Overview page displays key Job, KPI, and Event information for a specified Job while also linking to specific KPI reports.

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

### Job

Specifies the Job ID for which to display relevant information.

### System

Specifies the System ID for which the Job is associated.

### KPI

Specifies the KPI Calculation ID (OeeCalculationID) for which to display data.

### Behavior | MTBF Baseline Seconds

Determines the MTBF Baseline (in seconds) to be displayed on the MTBF Tile/Chart (when shown).

### Behavior | MTBF Target Seconds

Determines the MTBF Target (in seconds) to be displayed on the MTBF Tile/Chart (when shown).

### Behavior | MTrBF Baseline Seconds

Determines the MTrBF Target (in seconds) to be displayed on the MTrBF Tile/Chart (when shown).

### Behavior | MTTR Baseline Seconds

Determines the MTTR Target (in seconds) to be displayed on the MTTR Tile/Chart (when shown).

### Behavior | MTrBF Target Seconds

Determines the MTrBF Target (in seconds) to be displayed on the MTrBF Tile/Chart (when shown).

### Behavior | MTTR Target Seconds

Determines the MTTR Target (in seconds) to be displayed on the MTTR Tile/Chart (when shown).

### Column Widths

**Left** - Determines the width (1-12) of the left column of the page, typically where filters or details are displayed.

**Center** - Determines the width (1-12) of the center column of the page, typically where tabular data or charts are displayed.

**Right** - Determines the width (1-12) of the right column of the page, typically where selected data information is displayed.

### Column Widths | Tile

Specifies the width (1-12) of informational KPI Tile/links.

### Column Widths | Trend

Specifies the width (1-12) of the trend charts on the right side of the page.

## Content

### Allow

**Export** - Determines whether or not to display the Export button on the report and therefore allow the export of report data to Excel.

## Links

The following properties allow for the specification of link targets when clicking various elements on the Page. Any URL within the TrakSYS application (or external) can be specified. In some cases, QueryString parameters may be passed to the target using Values Keys that are available on this Page. Some link properties include a default URL that directs to a standard Page when the value is left empty (these defaults are specified below when applicable).

### Edit

Specifies an alternate link to the Discrete Job Edit form. If this value is blank, the default link is:

`?c=ETS.Application.Job.JobDiscreteNewEdit&JobID={JobID}&SystemID={SystemID}`

### Delete

Specifies an alternate link to the Discrete Job Delete form. If this value is blank, the default link is:

`?c=ETS.Application.Job.JobDiscreteDelete&JobID={JobID}`

### OEE

Specifies an alternate link to the OEE Overview report for Job. If this value is blank, the default link is:

`csharp?c=ETS.Application.Kpi.KpiOeeOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### Availability

Specifies an alternate link to the Availability Overview report for Job. If this value is blank, the default link is:

`?c=ETS.Application.Kpi.KpiAvailabilityOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### Performance

Specifies an alternate link to the Performance Overview report for Job. If this value is blank, the default link is:

`?c=ETS.Application.Kpi.KpiPerformanceOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### Quality

Specifies an alternate link to the Quality Overview report for Job. If this value is blank, the default link is:

`?c=ETS.Application.Kpi.KpiQualityOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### MTBF

Specifies an alternate link to the MTBF Overview report for Job. If this value is blank, the default link is:

`?c=ETS.Application.Kpi.KpiMtbfOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### MTrBF

Specifies an alternate link to the MTrBF Overview report for Job. If this value is blank, the default link is:

`?c=ETS.Application.Kpi.KpiMtrbfOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### MTTR

Specifies an alternate link to the MTTR Overview report for Job. If this value is blank, the default link is:

`csharp?c=ETS.Application.Kpi.KpiMttrOverview&SystemID={SystemID}&RangeIsUsed=0&JobID={JobID}&GroupBy={GroupBy}&AllowFilterInteraction=0&AllowSettingsInteraction=0`

### Show | Edit

Determines whether or not to enable the link to the Discrete Job Edit form when clicking the Edit button at the top of this page.

### Show | Delete

Determines whether or not to enable the link to the Discrete Job Delete dialog when clicking the Delete button at the top of this page.

### Show | OEE

Determines whether or not to enable the link to the OEE Overview report for the selected Job when clicking the OEE Tile.

### Show | Availability

Determines whether or not to enable the link to the Availability Overview report for the selected Job when clicking the Availability Tile.

### Show | Performance

Determines whether or not to enable the link to the Performance Overview report for the selected Job when clicking the Performance Tile.

### Show | Quality

Determines whether or not to enable the link to the Quality Overview report for the selected Job when clicking the Quality Tile.

### Show | MTBF

Determines whether or not to enable the link to the MTBF Overview report for the selected Job when clicking the MTBF Tile.

### Show | MTrBF

Determines whether or not to enable the link to the MTrBF Overview report for the selected Job when clicking the MTrBF Tile.

### Show | MTTR

Determines whether or not to enable the link to the MTTR Overview report for the selected Job when clicking the MTTR Tile.

## Charts

### Center Width

Determines the width (in pixels) of charts displayed in the center of the page.

### Center Height

Determines the height (in pixels) of charts displayed in the center of the page.

### Right Width

Determines the width (in pixels) of charts displayed on the right of the page.

### Right Height

Determines the height (in pixels) of charts displayed on the right of the page.

### Show | OEE

Determines whether or not to show the OEE informational Tile and Chart.

### Show | Availability

Determines whether or not to show the Availability informational Tile and Chart.

### Show | Performance

Determines whether or not to show the Performance informational Tile and Chart.

### Show | Quality

Determines whether or not to show the Quality informational Tile and Chart.

### Show | MTBF

Determines whether or not to show the MTBF informational Tile and Chart.

### Show | MTrBF

Determines whether or not to show the MTrBF informational Tile and Chart.

### Show | MTTR

Determines whether or not to show the MTTR informational Tile and Chart.

### Show | Production Count

Determines whether or not to show the Production Count informational Tile and Chart.

### Show | Events by Sub-System

Determines whether or not to show the Events by Sub-System Chart.

### Show | Events by Definition

Determines whether or not to show the Events by Definition Chart.

### Show | Events by Category

Determines whether or not to show the Events by Category Chart.

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
