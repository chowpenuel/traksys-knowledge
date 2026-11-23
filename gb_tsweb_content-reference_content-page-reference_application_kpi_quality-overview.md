# Quality Overview

The Quality Overview report displays aggregate and trend data for Quality in an interactive dashboard format.

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

### KPI Calculation

Specifies the OEE Calculation ID for which to display data.

### System

Specifies the System ID for which to display data.

### Date/Time Range

**Use in Query** - Determines whether or not to use the Date/Time Range values in the report query for returning data.

### Filters

**Start Date** - The Start Date of the range to be used in the report query (WHERE clause) for returning data.

**End Date** - The End Date of the range to be used in the report query (WHERE clause) for returning data.

**Shift** - The Shift ID to be used in the report query (WHERE clause) for returning data.

**Product** - The Product ID to be used in the report query (WHERE clause) for returning data.

**Job** - The Job ID to be used in the report query (WHERE clause) for returning data.

**Shift History** - The Shift HistoryID to be used in the report query (WHERE clause) for returning data.

**Allow Filter Interaction** - Determines whether or not to allow a report user to manipulate any of the reports filters. The is especially useful when linking to the report from another page and passing values using the query string or the Values Collection.

### Behavior

**Group By** - Specifies the default Group By selection for the report.

**Allow Settings Interaction** - Determines whether or not a report user can change the report settings. This is especially useful when linking to the report from another page and passing values using the query string or the Values Dictionary.

### Column Widths

**Left** - Determines the width (1-12) of the left column of the page, typically where filters or details are displayed.

**Center** - Determines the width (1-12) of the main center column of the page, typically where tabular data or charts are displayed.

**Center 1** - Determines the width (1-12) of the first column within the main center column of the page, typically where tabular data or charts are displayed.

**Center 2** - Determines the width (1-12) of the second column within the main center column of the page, typically where tabular data or charts are displayed.

**Center 3** - Determines the width (1-12) of the third column within the main center column of the page, typically where tabular data or charts are displayed.

**Right** - Determines the width (1-12) of the center column of the page, typically where tabular data or charts are displayed.

## Content

### Allow

**Export** - Determines whether or not to display the Export button on the report and therefore allow the export of report data to Excel.

## Charts

#### Trend Width

Specifies the width (in pixels) of the KPI Trend chart.

#### Trend Height

Specifies the height (in pixels) of the KPI Trend chart.

#### Event Width

Specifies the width (in pixels) of the Event charts.

#### Event Height

Specifies the height (in pixels) of the Event charts.

#### Event Top N

Specifies number of rows/columns to display on each of the Event charts.

#### Show | Events by Sub-System

Determines whether or not to show the Events by Sub-System chart on the page.

#### Show | Events by Definition

Determines whether or not to show the Events by Definition chart on the page.

#### Show | Events by Category

Determines whether or not to show the Events by Category chart on the page.

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
