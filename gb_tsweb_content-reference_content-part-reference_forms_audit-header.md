# Audit Header

Displays the user interface form inputs to collect Audit signature and notes information. When a form containing the Audit Header part is posted, a series of values is placed into the Values Dictionary. These values are essentially the properties of an `ETS.Core.Api.Data.DbAuditHeader` model object (with a prefix specified by the Values Prefix property below).

## General

### Caption

Specifies a text caption that appears above the part's controls.

### Icon

Specifies an optional icon that appears to the left of the part caption.

### Show Separator

Determines if a horizontal line separator is displayed below the part's caption.

### Behavior | Value Prefix

Specifies a prefix that is appended to the beginning of each of the part's value elements when the form is posted.

### Behavior | Entity Type Name

Specifies the Entity that is being signed for. The Entity Type Name is essentially the TrakSYS database table name (minus the "t" prefix). For example, when signing for a change to an tEvent record, the Entity Type Name would be "Event". The Entity Type Name controls where some of the property values below are inherited from.

### Behavior | Signature Type

Determines which types of user name and password input controls are rendered and the type of validation that is applied to the signature data when the form is posted.

**Inherit** - Inherit the setting from this property from the TrakSYS Audit Settings (set in Installation Manager) for the selected Entity Type.

**None** - No signature is required. No user name will be recorded.

**Auto** - No signature is required. The user name will be automatically copied from the logged in user credentials.

**Name Only** - Only a user name input is rendered. There is no validation applied (anything can be entered).

**Single** - A single set of user name and password inputs are rendered. The user name and password are validated against the Users defined in the TrakSYS configuration. A signing user must also be a part of a Role with the IsAuditor permission.

**Dual** - Two sets of user name and password inputs are rendered. The user names and passwords are validated against the Users defined in the TrakSYS configuration. A signing user must also be a part of a Role with the IsAuditor permission.

### Behavior | Reason

Specifies the (initial) reason description that will be displayed to the user as an explanation of why the signature is required. This value (if unchanged) will be posted back and saved with the signature data.

### Behavior | Reason Mode

Specifies how the signature reason (purpose for requiring signature) is displayed.

**Invisible** - No reason is displayed. If the Reason property is used, the values is passed back to the signature and saved automatically.

**Read Only** - The specified Reason is displayed to the user on the form, however it cannot be changed.

**Text Box** - The specified Reason is pre-populated in a text box, but can be changed by the user before the form is posted.

**Drop Down** - The specified Reason is pre-populated in a list of choices, but can be changed by the user before the form is posted.

### Behavior | Reason Source Values Key

When the Reason Mode property is set to Drop Down, a drop down input is rendered with a list of items (strings) from the Values Dictionary specified by this Key. The Values Dictionary item specified must contain either a `.NET` DataSet or DataReader object, or an `IEnumerable` list of objects.

### Behavior | Notes Type

Determines which types of notes input control is rendered and the type of validation that is applied when the form is posted.

**Inherit** - Inherit the setting from this property from the TrakSYS Audit Settings (set in Installation Manager) for the selected Entity Type.

**Hide** - No notes input is displayed or required.

**Optional** - A notes input is displayed, however it does not require a value.

**Required** - A notes input is displayed and an entry is required when the form is posted.

## Advanced

### CSS Class

Any CSS class values added to this property will be rendered to the part's HTML. While the CSS is typically rendered to an outer DIV element, the exact HTML element that this CSS is added to is part specific.

### Visible

When false, this part will NOT be rendered to the browser. For most visual parts, this means that any processing (Values Dictionary manipulation, data retrieval, etc...) will not be executed. For Data Table parts, setting the Visible to false will still allow the part to execute its query and place its resultant dataset in the Values dictionary, however any visual debugging elements will not be rendered.

### Initialization Order

Indicates the order that this part will be loaded and executed on the containing page. This value also indicates which script method (ContentPage\_PartPreInitXX) should be used to initialize properties just before the part is loaded. If this property is left blank, each part will load using its own default Initialization Order.

### Initialization Order Sub

Indicates the order that this part will be loaded and executed on the containing page. This property value is used in conjunction with the Initialization Order value to create the final load sequence (the Initialization Order Sub value is used as a decimal value added to the Initialization Order). For example if the Initialization Order is 3 and the Order Sub is 2, the actual load order would be 3.2.

If this property is left blank, each part will load using its own default Initialization Order Sub (typically 1).
