# SPC Variable Overview

The SPC Variable Overview page is a complete SPC overview for a specified Variable type Sample Definition. It contains several Variable SPC charts, a tabular view of recent Sample Sub Group captures, links to manually add new Sample measurements, and some real-time SPC capability metric displays.

{% hint style="info" %}
A minimum of 30 Sample Sub Groups is required in order for built-in Rule Violations to trigger. If less than 30 are provided, the violations will not trigger and they will not be displayed on the page.
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

### Sample Definition

Specifies the Sample Definition ID for which to display relevant information.

### Last N Sub-Groups

Specifies the maximum number of recent Sub-Groups to display in the charts and to be used in the calculations displayed on the page.

### Current Product

Determines whether or not to display data for the current Product.

### Current Job

Determines whether or not to display data for the current Job.

### Behavior | Auto Calculate Limits

Determines whether or not to automatically calculate limits based on the given data.

### Column Widths

**Left** - Determines the width (1-12) of the left column of the page, typically where filters or details are displayed.

**Center** - Determines the width (1-12) of the center column of the page, typically where tabular data or charts are displayed.

**Right** - Determines the width (1-12) of the right column of the page, typically where selected data information is displayed.

## Content

### List Last N Sub-Groups

Determines the number of Sub-Groups to display in the List on the right side of the Page.

### Calculations Low Value

Specifies the Low Value for determining the color of the Calculation Tiles (i.e. red if calculated value is out of range).

### Calculations High Value

Specifies the High Value for determining the color of the Calculation Tiles (i.e. red if calculated value is out of range).

### Allow | Job Details

Determines whether or not to display Job details on the left side of the page.

### Allow | Pp

Determines whether or the to show the Pp calculation Type on the left side of the page.

### Allow | Ppk

Determines whether or the to show the Ppk calculation Type on the left side of the page.

### Allow | Cp

Determines whether or the to show the Cp calculation Type on the left side of the page.

### Allow | Cpk

Determines whether or the to show the Cpk calculation Type on the left side of the page.

## Links

The following properties allow for the specification of link targets when clicking various elements on the Page. Any URL within the TrakSYS application (or external) can be specified. In some cases, QueryString parameters may be passed to the target using Values Keys that are available on this Page. Some link properties include a default URL that directs to a standard Page when the value is left empty (these defaults are specified below when applicable).

### Sub-Group New

Specifies an alternate link to the SPC Variable Sample Sub-Group New form. If this value is blank, the default link is:

`?c=ETS.Application.Spc.SpcVariableSubGroupNewEdit&SampleDefinitionID=SampleDefinitionID}`

### Sub-Group Edit

Specifies an alternate link to the SPC Variable Sample Sub-Group Edit form. If this value is blank, the default link is:

`?c=ETS.Application.Spc.SpcVariableSubGroupNewEdit&SampleSubGroupID=SampleSubGroupID}`

### Sub-Group Delete

Specifies an alternate link to the SPC Sub-Group Delete dialog. If this value is blank, the default link is:

`?c=ETS.Application.Spc.SpcSubGroupDelete&SampleSubGroupID={SampleSubGroupID}`

### Sub-Group List

Specifies an alternate link to the SPC Variable Sub-Group List. If this value is blank, the default link is:

`?c=ETS.Application.Spc.SpcVariableSubGroupList&SampleDefinitionID=SampleDefinitionID}`

### Sub-Group Point

Specifies an alternate link to the SPC Variable Overview page with the Selected Sample Sub-Group Value highlighted. If this value is blank, the default link is:

`self:?SelectedSampleSubGroupID={SampleSubGroupID}`

### Sub-Group Violation

Specifies an alternate link to the SPC Variable Overview page with the Selected Sample Sub-Group Violation highlighted. If this value is blank, the default link is:

`self:?SelectedSampleSubGroupID={SampleSubGroupID}`

### Show | Sub-Group New

Determines whether or not to enable the link to the Sub-Group New form when clicking the New button above the Sub-Groups List.

### Show | Sub-Group Edit

Determines whether or not to enable the link to the Sub-Group Edit form when clicking the Edit icon on each Sub-Group List Item row.

### Show | Sub-Group Delete

Determines whether or not to enable the link to the Sub-Group Delete dialog when clicking the Delete icon each Sub-Group List Item row.

### Show | Sub-Group List

Determines whether or not to enable the link to the Sub-Group List when clicking the List button above the Sub-Groups List.

### Show | Sub-Group Point

Determines whether or not to enable the link when clicking a Sub-Group Point on the charts.

### Show | Sub-Group Violation

Determines whether or not to enable the link when clicking a Sub-Group Violation on the charts.

## Charts

### Width

Determines the width (in pixels) of charts on the page.

### Height

Determines the height (in pixels) of charts on the page.

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
